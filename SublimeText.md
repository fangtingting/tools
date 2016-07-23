## 安装Sublime Text
1、下载地址：[http://www.sublimetext.com/3](http://www.sublimetext.com/3)

2、安装Package Control(Sublime Text下View -->Show Console输入)：[https://packagecontrol.io/installation](https://packagecontrol.io/installation)

安装插件快捷键：Ctrl ／ Cmd ＋ P


## 插件推荐

1、Emmet：快速编写 HTML/CSS 代码的方案

2、AllAutocomplete：会搜索所有打开的文件来寻找匹配的提示词

3、ColorPicker：一个颜色选择器，只要按下Ctrl / Cmd + Shift + C 快捷键

4、DocBlokr：帮助你创造你的代码注释，用 /* 或 /** 开始一行代码

5、BracketHighlighter：类似于代码匹配，可以匹配括号，引号等符号内的范围

6、SideBarEnhancement：为侧边栏添加很多额外的功能

7、jQuery：这个插件提供了额外的语法高亮和几乎所有jQuery方法的片段。通过输入方法名称并选择合适的匹配就可以访问这些片段

8、SublimeLinter：代码校验插件，支持HTML、CSS、JS、PHP、Java、C++等16种语言

9、Tag：HTML／XML标签缩进、补全和校验

## sublime text配置

1、Preference > Key binding - user

> //代码缩进（系统自带）

> { "keys": ["ctrl+shift+r"], "command": "reindent" } 

2、Preference > Settings - User

>   "tab_size": 2

>  "translate_tabs_to_spaces": true

## sublime text解决linux无法输入中文问题

1、安装输入法：[http://pinyin.sogou.com/linux/](http://pinyin.sogou.com/linux/)

2、保存代码到sublime_imfix.c里

    /*
    sublime-imfix.c
    Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
    By Cjacker Huang <jianzhong.huang at i-soft.com.cn>

    gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
    LD_PRELOAD=./libsublime-imfix.so sublime_text
    */
    #include <gtk/gtk.h>
    #include <gdk/gdkx.h>
    typedef GdkSegment GdkRegionBox;

    struct _GdkRegion
    {
      long size;
      long numRects;
      GdkRegionBox *rects;
      GdkRegionBox extents;
    };

    GtkIMContext *local_context;

    void
    gdk_region_get_clipbox (const GdkRegion *region,
                GdkRectangle    *rectangle)
    {
      g_return_if_fail (region != NULL);
      g_return_if_fail (rectangle != NULL);

      rectangle->x = region->extents.x1;
      rectangle->y = region->extents.y1;
      rectangle->width = region->extents.x2 - region->extents.x1;
      rectangle->height = region->extents.y2 - region->extents.y1;
      GdkRectangle rect;
      rect.x = rectangle->x;
      rect.y = rectangle->y;
      rect.width = 0;
      rect.height = rectangle->height;
      //The caret width is 2;
      //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
      if(rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
            gtk_im_context_set_cursor_location(local_context, rectangle);
      }
    }

    //this is needed, for example, if you input something in file dialog and return back the edit area
    //context will lost, so here we set it again.

    static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
    {
        XEvent *xev = (XEvent *)xevent;
        if(xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
           GdkWindow * win = g_object_get_data(G_OBJECT(im_context),"window");
           if(GDK_IS_WINDOW(win))
             gtk_im_context_set_client_window(im_context, win);
        }
        return GDK_FILTER_CONTINUE;
    }

    void gtk_im_context_set_client_window (GtkIMContext *context,
              GdkWindow    *window)
    {
      GtkIMContextClass *klass;
      g_return_if_fail (GTK_IS_IM_CONTEXT (context));
      klass = GTK_IM_CONTEXT_GET_CLASS (context);
      if (klass->set_client_window)
        klass->set_client_window (context, window);

      if(!GDK_IS_WINDOW (window))
        return;
      g_object_set_data(G_OBJECT(context),"window",window);
      int width = gdk_window_get_width(window);
      int height = gdk_window_get_height(window);
      if(width != 0 && height !=0) {
        gtk_im_context_focus_in(context);
        local_context = context;
      }
      gdk_window_add_filter (window, event_filter, context);
    }

3、编译代码

	//安装编译环境
	sudo apt-get install build-essential  libgtk2.0-dev

	gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC

4、将libsublime-imfix.so拷贝到sublime_text所在文件夹

	sudo mv libsublime-imfix.so /opt/sublime_text_2/

5、修改/usr/bin/subl

	SUBLIME_HOME="/opt/sublime_text_2"
	LD_LIB=$SUBLIME_HOME/libsublime-imfix.so 
	sh -c "LD_PRELOAD=$LD_LIB $SUBLIME_HOME/sublime_text $@"

6、重启sublime text
