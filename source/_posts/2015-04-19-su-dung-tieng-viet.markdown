---
layout: post
title: "Sử dụng tiếng viêt làm tiêu đề"
date: 2015-04-19 21:13:47 +0700
comments: true
categories: 
- test
- coderay
- tech
---
for testing some code
{% coderay lang:cplusplus linenos:false This is a great example! http://hddt.github.io My Blog %}
#include <SFML/Window.hpp>
#include <SFML/Graphics.hpp>
#include <SFML/Audio.hpp>

int main(int argc, char* argv[])
{
  sf::RenderWindow window(sf::VideoMode(640, 480), "SFML Music test");
  sf::Music music;
  music.openFromFile("menu.ogg");
  music.setLoop(true);
  music.play();

  while (window.isOpen()) {
    window.clear();
  }
}
{% endcoderay %}
<!--more-->

## Just tesing some code, Are you ready?

{% coderay lang:HTML linenos:false This is a great example! http://hddt.github.io My Blog %}
<div data-slick="">
    <div data-slick-panel="slick-panel-1">
        <img class="th" src="assets/demo/demo1.jpg">
    </div>
    <div data-slick-panel="slick-panel-2">
        <img class="th" src="assets/demo/demo2.jpg">
    </div>
</div>

<div class="slick-panels-wrapper">
    <div class="slick-panel-1 slick-panel">
        <h3>HEADER 1</h3><img class="th" src="assets/demo/demo1.jpg">
    </div>
    <div class="slick-panel-2 slick-panel">
        <h3>HEADER 2</h3><img class="th" src="assets/demo/demo2.jpg">
    </div>
</div>

<script type="text/javascript">

$(function(){
            $('[data-slick]').slick({
              centerMode: true,
              slidesToShow: 5,
              focusOnSelect: true,
              responsive: [
                {
                  breakpoint: 1024,
                  settings: {
                    focusOnSelect: true,
                    slidesToShow: 3
                  }
                },
                {
                  breakpoint: 640,
                  settings: {
                    arrows: false,
                    slidesToShow: 1
                  }
                }
              ]
            });
            
            var currentSlide = $('[data-slick]').slick('slickCurrentSlide');         
            var currentPanel = $('[data-slick-index="' + currentSlide + '"]').attr('data-slick-panel');
            $('.slick-panel').hide();
            $("." + currentPanel).show();
            
            $('[data-slick]').on('afterChange', function(slick, currentSlide){
                var currentSlide = $('[data-slick]').slick('slickCurrentSlide');         
                var currentPanel = $('[data-slick-index="' + currentSlide + '"]').attr('data-slick-panel');
                $('.slick-panel').hide();
                $("." + currentPanel).show();
            });
            
        });

</script>
{% endcoderay %}

{% coderay lang:ruby linenos:false This is a great example! http://hddt.github.io My Blog %}
// ruby
apply plugin: 'findbugs'
apply plugin: 'pmd'

check.dependsOn 'pmd', 'findbugs'

task pmd(type: Pmd) {
    ignoreFailures = true
    ruleSetFiles = files("${project.rootDir}/config/quality/pmd/pmd-ruleset.xml")
    ruleSets = []

    source fileTree("src/")
    include '**/*.java'
    exclude '**/gen/**'

    reports {
        xml.enabled = true
        html.enabled = true
    }
}

findbugs {
    sourceSets = []
    ignoreFailures = true
}

task findbugs(type: FindBugs) {
    excludeFilter file("${project.rootDir}/config/quality/findbugs/findbugs-filter.xml")
    classes = fileTree("${project.rootDir}/build/intermediates/classes/debug/")
    source = fileTree("src/")
    classpath = files()
    effort = 'max'

    reports {
        xml.enabled = true
        html.enabled = false
    }
}

{% endcoderay %}

{% coderay lang:cplusplus linenos:false This is a great example! http://hddt.github.io My Blog %}
// cplusplus
#include <iostream>
#include <SDL.h>
#include <SDL_opengl.h>
#include <CEGUI/CEGUI.h>
#include <CEGUI/RendererModules/OpenGL/GLRenderer.h>
#include <CEGUI/XMLParserModules/Expat/XMLParser.h>
#include <CEGUI/ImageCodecModules/DevIL/ImageCodec.h>

int main(int, char**)
{
  /***************************************
   * Init SDL
   ***************************************/

  if (SDL_Init(SDL_INIT_EVERYTHING) != 0){
    std::cout << "SDL_Init Error: " << SDL_GetError() << std::endl;
    SDL_Quit();
    return 1;
  }

  SDL_Window* p_window = SDL_CreateWindow("Test window", 100, 100, 640, 480, SDL_WINDOW_SHOWN | SDL_WINDOW_OPENGL);
  if (!p_window) {
    std::cerr << "failed to set up window." << std::endl;
    SDL_Quit();
    return 2;
  }

  SDL_ShowCursor(0);

  SDL_Renderer* p_sdl_renderer = SDL_CreateRenderer(p_window, -1, SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC);
  if (!p_sdl_renderer) {
    SDL_DestroyWindow(p_window);
    SDL_Quit();
    std::cerr << "Faield to set up renderer." << std::endl;
    return 3;
  }

  /***************************************
   * Init CEGUI
   ***************************************/

  //CEGUI::OpenGLRenderer& renderer = CEGUI::OpenGLRenderer::bootstrapSystem();
  CEGUI::OpenGLRenderer& renderer = CEGUI::OpenGLRenderer::create();
  CEGUI::DefaultResourceProvider* p_provider = new CEGUI::DefaultResourceProvider();
  CEGUI::ExpatParser* p_xml_parser = new CEGUI::ExpatParser();
  CEGUI::DevILImageCodec* p_imgcodec = new CEGUI::DevILImageCodec();

  CEGUI::System::create(renderer, p_provider, p_xml_parser, p_imgcodec, NULL);

  p_provider->setResourceGroupDirectory("schemes", "/usr/share/cegui-0/schemes/");
  p_provider->setResourceGroupDirectory("imagesets", "/usr/share/cegui-0/imagesets/");
  p_provider->setResourceGroupDirectory("fonts", "/usr/share/cegui-0/fonts/");
  p_provider->setResourceGroupDirectory("layouts", "/usr/share/cegui-0/layouts/");
  p_provider->setResourceGroupDirectory("looknfeels", "/usr/share/cegui-0/looknfeel/");
  p_provider->setResourceGroupDirectory("lua_scripts", "/usr/share/cegui-0/lua_scripts/");

  /* Now tell each of CEGUI’s resource-consuming classes (the "*Manager" classes)
   * which group of the filesystem provider to ask for its stuff. */
  CEGUI::ImageManager::setImagesetDefaultResourceGroup("imagesets");
  CEGUI::Font::setDefaultResourceGroup("fonts");
  CEGUI::Scheme::setDefaultResourceGroup("schemes");
  CEGUI::WidgetLookManager::setDefaultResourceGroup("looknfeels");
  CEGUI::WindowManager::setDefaultResourceGroup("layouts");
  CEGUI::ScriptModule::setDefaultResourceGroup("lua_scripts");

  CEGUI::SchemeManager::getSingleton().createFromFile("TaharezLook.scheme");
  CEGUI::FontManager::getSingleton().createFromFile("DejaVuSans-12.font");
  CEGUI::System::getSingleton().getDefaultGUIContext().setDefaultFont("DejaVuSans-12");
  CEGUI::System::getSingleton().getDefaultGUIContext().getMouseCursor().setDefaultImage("TaharezLook/MouseArrow");

  // Tell CEGUI how large our Window is. Forget this and you’ll never see anything.
  CEGUI::System::getSingleton().notifyDisplaySizeChanged(CEGUI::Sizef(640, 480));

  CEGUI::WindowManager& wmgr = CEGUI::WindowManager::getSingleton();
  CEGUI::Window* p_cegui_rootwin = wmgr.createWindow("DefaultWindow", "root");
  CEGUI::System::getSingleton().getDefaultGUIContext().setRootWindow(p_cegui_rootwin);

  CEGUI::FrameWindow* p_testframe = static_cast<CEGUI::FrameWindow*>(wmgr.createWindow("TaharezLook/FrameWindow", "testWindow"));
  p_testframe->setPosition(CEGUI::UVector2(CEGUI::UDim(0.25, 0.0), CEGUI::UDim(0.25, 0.0f)));
  p_testframe->setSize(CEGUI::USize(CEGUI::UDim(0.5f, 0.0f), CEGUI::UDim(0.5f, 0.0f)));
  p_testframe->setText("Hello, World!");
  p_cegui_rootwin->addChild(p_testframe);

  glClearColor(0, 0, 0, 255);

  SDL_Surface* p_image = SDL_LoadBMP("../hello.bmp");
  SDL_Texture* p_imgtexture = SDL_CreateTextureFromSurface(p_sdl_renderer, p_image);
  SDL_FreeSurface(p_image);
  p_image = NULL;

  /***************************************
   * Main loop
   ***************************************/
  bool quit = false;
  SDL_Event evt;
  while (!quit) {
    // Grab all events from the queue
    while (SDL_PollEvent(&evt)) {
      if (evt.type == SDL_QUIT) {
        quit = true;
      }
      else {
        std::cout << "Unknown event received." << std::endl;
      }
    }

    SDL_RenderClear(p_sdl_renderer);
    SDL_RenderCopy(p_sdl_renderer, p_imgtexture, NULL, NULL);
    SDL_RenderPresent(p_sdl_renderer);

    SDL_GLContext context = SDL_GL_CreateContext(p_window);
    glClear(GL_COLOR_BUFFER_BIT);
    CEGUI::System::getSingleton().renderAllGUIContexts();
    SDL_GL_SwapWindow(p_window);
    SDL_GL_DeleteContext(context);
  }

  /***************************************
   * Cleanup
   ***************************************/

  CEGUI::System::destroy();
  CEGUI::OpenGLRenderer::destroy(renderer);
  delete p_imgcodec;
  delete p_xml_parser;
  delete p_provider;

  SDL_DestroyTexture(p_imgtexture);
  SDL_DestroyRenderer(p_sdl_renderer);
  SDL_DestroyWindow(p_window);
  SDL_Quit();
  return 0;
}

{% endcoderay %}

{% coderay lang:diff linenos:false This is a great example! http://hddt.github.io My Blog %}
--- a/application_templates/SDL2.cpp	Sun Jan 04 18:31:27 2015 +0100
+++ b/application_templates/SDL2.cpp	Sat Mar 14 09:43:51 2015 +0100
@@ -40,7 +40,8 @@
 #include <iostream>
 
 #include <CEGUI/CEGUI.h>
-#include <CEGUI/RendererModules/OpenGL/GL3Renderer.h>
+//#include <CEGUI/RendererModules/OpenGL/GL3Renderer.h>
+#include <CEGUI/RendererModules/OpenGL/GLRenderer.h>
 
 #include <SDL.h>
 #include <SDL_opengl.h>
@@ -161,7 +162,7 @@
     using namespace CEGUI;
 
     // create renderer and enable extra states
-    OpenGL3Renderer& cegui_renderer = OpenGL3Renderer::create(Sizef(800.f, 600.f));
+    OpenGLRenderer& cegui_renderer = OpenGLRenderer::create(Sizef(800.f, 600.f));
     cegui_renderer.enableExtraStateSettings(true);
 
     // create CEGUI system object
@@ -237,7 +238,8 @@
     }
 }
 
-int SDL_main(int argc, char* argv[])
+//int SDL_main(int argc, char* argv[])
+int main(int argc, char* argv[])
 {
     using namespace CEGUI;
 
@@ -260,7 +262,7 @@
     SDL_Event event;
     float time = SDL_GetTicks() / 1000.f;
 
-    OpenGL3Renderer* renderer = static_cast<OpenGL3Renderer*>(System::getSingleton().getRenderer());
+    OpenGLRenderer* renderer = static_cast<OpenGLRenderer*>(System::getSingleton().getRenderer());
 
     // repeat until a quit is requested
     while (!quit && !SDL_QuitRequested())
@@ -335,7 +337,7 @@
 
     // destroy system and renderer
     System::destroy();
-    OpenGL3Renderer::destroy(*renderer);
+    OpenGLRenderer::destroy(*renderer);
     renderer = 0;
 
     // delete SDL GL context
@@ -348,4 +350,4 @@
     SDL_Quit();
 
     return 0;
-}
\ No newline at end of file
+}

{% endcoderay %}

{% coderay lang:c linenos:false This is a great example! http://hddt.github.io My Blog %}
// c
#include <stdio.h>

void Nhap(float a[], int n)
{
	printf("Nhap lan luot cac he so:\n");
	for (int i = 0; i <= n; ++i)
	{
		scanf("%f", &a[i]);
	}
}

// Ham tinh dung de quy
void HoocnerRecurison(float a[], int n, float c)
{
	if (n==0) return;
	for (int i = 0;i < n;i++)
		a[i+1] = a[i] *c +a[i+1];
	HoocnerRecurison(a,n-1,c);
}

// Ham tinh khong dung de quy
void Hoocner(float a[], int n, float c)
{
 	for (int i = n; i > 0; --i)
	 	for (int j=0; j<i; j++)
	 		a[j+1] = a[j]*c + a[j+1];
}

void KetQua(float a[], int n, float c)
{
	printf("Cac he so cua phuong trinh\n");
	for (int i = 0; i <= n; ++i)
	{
		printf("%.2f  ", a[i]);
	}
}

int main()
{
	int n, c;
	float a[100];
	printf("Nhap bac phuong trinh: n= ");
	scanf("%d",&n);
	Nhap(a,n);
	printf("Nhap gia tri c: \n");
	scanf("%d", &c);
	HoocnerRecurison(a, n, c);
	KetQua(a,n,c);
	return 0;
}
{% endcoderay %}

{% coderay lang:Python linenos:false This is a great example! http://hddt.github.io My Blog %}
# Python
from rest_framework import serializers
from snippets.models import Snippet
from django.contrib.auth.models import User


class SnippetSerializer(serializers.HyperlinkedModelSerializer):
    owner = serializers.ReadOnlyField(source='owner.username')
    highlight = serializers.HyperlinkedIdentityField(view_name='snippet-highlight', format='html')

    class Meta:
        model = Snippet
        fields = ('url', 'highlight', 'owner',
                  'title', 'code', 'linenos', 'language', 'style')


class UserSerializer(serializers.HyperlinkedModelSerializer):
    snippets = serializers.HyperlinkedRelatedField(many=True, view_name='snippet-detail', read_only=True)

    class Meta:
        model = User
        fields = ('url', 'username', 'snippets')
{% endcoderay %}

{% coderay lang:YAML linenos:false %}
# YAML
root: /
permalink: /blog/:year/:month/:title/
source: source
destination: public
plugins: plugins
code_dir: downloads/code
category_dir: blog/categories
markdown: kramdown
kramdown:
  use_coderay: true
  coderay:
    coderay_line_numbers: table
    coderay_css: class
highlighter: pygments # default python pygments have been replaced by pygments.rb
{% endcoderay %}

{% coderay lang:JSON linenos:false This is a great example! http://hddt.github.io My Blog %}
{
    "Books": [
        {
            "Description": "If you're ready to create web pages more complex than what you can build with HTML and CSS, Head First PHP & MySQL is the ultimate learning guide to building dynamic, database-driven websites using PHP and MySQL. Packed with real-world examples, this ...", 
            "ID": 947185260, 
            "Image": "http://s.it-ebooks-api.info/3/head_first_php__mysql.jpg", 
            "Title": "Head First PHP & MySQL", 
            "isbn": "9780596006303"
        }, 
        {
            "Description": "If you know HTML, this guide will have you building interactive websites quickly. You'll learn how to create responsive, data-driven websites with PHP, MySQL, and JavaScript, regardless of whether you already know how to program. Discover how the pow ...", 
            "ID": 1283537446, 
            "Image": "http://s.it-ebooks-api.info/3/learning_php_mysql_and_javascript.jpg", 
            "SubTitle": "A Step-by-Step Guide to Creating Dynamic Websites", 
            "Title": "Learning PHP, MySQL, and JavaScript", 
            "isbn": "9780596157135"
        }, 
        {
            "Description": "PHP & MySQL: Novice to Ninja, 5th Edition is a hands-on guide that will help you build your first database driven website. In the fifth edition of this best-selling book, you'll learn how to use PHP (used on 20 million sites worldwide) to build your ...", 
            "ID": 4061324578, 
            "Image": "http://s.it-ebooks-api.info/7/php__mysql_novice_to_ninja_5th_edition.jpg", 
            "SubTitle": "The Easy Way to Build Your Own Database Driven Website", 
            "Title": "PHP & MySQL: Novice to Ninja, 5th Edition", 
            "isbn": "9780987153081"
        }, 
        {
            "Description": "Learn how to build interactive, data-driven websites - even if you don't have any previous programming experience. If you know how to build static sites with HTML, this popular guide will help you tackle dynamic web programming. You'll get a thorough ...", 
            "ID": 1290301462, 
            "Image": "http://s.it-ebooks-api.info/3/learning_php_mysql_javascript_and_css_2nd_edition.jpg", 
            "SubTitle": "A Step-by-Step Guide to Creating Dynamic Websites", 
            "Title": "Learning PHP, MySQL, JavaScript, and CSS, 2nd Edition", 
            "isbn": "9781449319267"
        }, 
        {
            "Description": "In just a short time, you can learn how to use PHP, MySQL, and Apache together to create dynamic, interactive websites and applications using the three leading open-source web development technologies. Using a straightforward, step-by-step approach, ...", 
            "ID": 2594711238, 
            "Image": "http://s.it-ebooks-api.info/12/sams_teach_yourself_php_mysql_and_apache_all_in_one_5th_edition.jpg", 
            "Title": "Sams Teach Yourself PHP, MySQL and Apache All in One, 5th Edition", 
            "isbn": "9780672335433"
        }, 
        {
            "Description": "Build interactive, data-driven websites with the potent combination of open-source technologies and web standards, even if you only have basic HTML knowledge. With this popular hands-on guide, you'll tackle dynamic web programming with the help of to ...", 
            "ID": 1967945201, 
            "Image": "http://s.it-ebooks-api.info/3/learning_php_mysql_javascript_css__html5_3rd_edition.jpg", 
            "SubTitle": "A Step-by-Step Guide to Creating Dynamic Websites", 
            "Title": "Learning PHP, MySQL, JavaScript, CSS & HTML5, 3rd Edition", 
            "isbn": "9781491949467"
        }, 
        {
            "Description": "Build interactive, data-driven websites with the potent combination of open-source technologies and web standards, even if you have only basic HTML knowledge. With this popular hands-on guide, you'll tackle dynamic web programming with the help of to ...", 
            "ID": 1953139307, 
            "Image": "http://s.it-ebooks-api.info/3/learning_php_mysql__javascript_4th_edition.jpg", 
            "SubTitle": "With jQuery, CSS & HTML5", 
            "Title": "Learning PHP, MySQL & JavaScript, 4th Edition", 
            "isbn": "9781491918661"
        }, 
        {
            "Description": "If you can build websites with CSS and JavaScript, this book takes you to the next level-creating dynamic, database-driven websites with PHP and MySQL. Learn how to build a database, manage your content, and interact with users through queries and we ...", 
            "ID": 2279690981, 
            "Image": "http://s.it-ebooks-api.info/3/php__mysql_the_missing_manual.jpg", 
            "Title": "PHP & MySQL: The Missing Manual", 
            "isbn": "9780596515867"
        }, 
        {
            "Description": "Build Your Own Database Driven Web Site Using PHP &amp; MySQL, 4th Edition is a practical, hands-on guide to learning all the tools, principles, and techniques needed to build a fully functional database driven web site using PHP &amp; MySQL. This bo ...", 
            "ID": 441392374, 
            "Image": "http://s.it-ebooks-api.info/7/build_your_own_database_driven_web_site_using_php.jpg", 
            "Title": "Build Your Own Database Driven Web Site Using PHP & MySQL, 4th Edition", 
            "isbn": "9780980576818"
        }, 
        {
            "Description": "Beginning PHP and MySQL: From Novice to Professional, Fourth Edition is a major update of W. Jason Gilmore's authoritative book on PHP and MySQL. The fourth edition includes complete coverage of PHP 5.3 features, including namespacing, an update of A ...", 
            "ID": 225821771, 
            "Image": "http://s.it-ebooks-api.info/6/beginning_php_and_mysql_from_novice_to_professional_4th_edition.jpg", 
            "SubTitle": "From Novice to Professional", 
            "Title": "Beginning PHP and MySQL, 4th Edition", 
            "isbn": "9781430231141"
        }
    ], 
    "Error": "0", 
    "Page": 1, 
    "Time": 0.0046, 
    "Total": "180"
}

{% endcoderay %}

{% coderay lang:XML linenos:false  %}
<macrodef name="create_manifest">
        <attribute name="jar.classname" />
        <sequential>
            <manifest file="jar_temp/META-INF/MANIFEST.MF">
                <attribute name="Manifest-Version" value="1.0" />
                <attribute name="Version" value="3.4" />
                <attribute name="Company" value="Pubnub" />
                <attribute name="Project" value="pubnub-api" />
                <attribute name="Java-Version" value="${java.version}" />
                <attribute name="Rsrc-Class-Path" value="./ bcprov-jdk15on-1.47.jar commons-cli-1.2.jar json-simple-1.1.1.jar json-20090211.jar slf4j-api-1.7.5.jar slf4j-simple-1.7.5.jar" />
                <attribute name="Class-Path" value="." />
                <attribute name="Rsrc-Main-Class" value="@{jar.classname}" />
                <attribute name="Main-Class" value="org.eclipse.jdt.internal.jarinjarloader.JarRsrcLoader" />
            </manifest>
        </sequential>
    </macrodef>
{% endcoderay %}

{% coderay lang:Java linenos:false This is a great example! %}
package com.pubnub.api;

import java.io.ByteArrayOutputStream;
import java.util.zip.GZIPInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.ProtocolException;
import java.net.SocketTimeoutException;
import java.net.URL;
import java.util.Enumeration;
import java.util.Hashtable;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import com.pubnub.api.PubnubException;
import static com.pubnub.api.PubnubError.*;

class HttpClientCore extends HttpClient {
    private int requestTimeout = 310000;
    private int connectionTimeout = 5000;
    HttpURLConnection connection;
    protected static Logger log = new Logger(Worker.class);

    private void init() {
        HttpURLConnection.setFollowRedirects(true);
    }

    public HttpClientCore(int connectionTimeout, int requestTimeout, Hashtable headers) {
        init();
        this.setRequestTimeout(requestTimeout);
        this.setConnectionTimeout(connectionTimeout);
        this._headers = headers;
    }

    public int getRequestTimeout() {
        return requestTimeout;
    }

    public void setRequestTimeout(int requestTimeout) {
        this.requestTimeout = requestTimeout;
    }

    public int getConnectionTimeout() {
        return connectionTimeout;
    }

    public void setConnectionTimeout(int connectionTimeout) {
        this.connectionTimeout = connectionTimeout;
    }

    public boolean isRedirect(int rc) {
        return (rc == HttpURLConnection.HTTP_MOVED_PERM
                || rc == HttpURLConnection.HTTP_MOVED_TEMP || rc == HttpURLConnection.HTTP_SEE_OTHER);
    }

    public boolean checkResponse(int rc) {
        return (rc == HttpURLConnection.HTTP_OK || isRedirect(rc));
    }

    public boolean checkResponseSuccess(int rc) {
        return (rc == HttpURLConnection.HTTP_OK);
    }

    private static String readInput(InputStream in) throws IOException {
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        byte bytes[] = new byte[1024];

        int n = in.read(bytes);

        while (n != -1) {
            out.write(bytes, 0, n);
            n = in.read(bytes);
        }

        return new String(out.toString());
    }

    public HttpResponse fetch(String url) throws PubnubException, SocketTimeoutException {
        return fetch(url, null);
    }
{% endcoderay %}