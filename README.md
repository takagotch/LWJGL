### lwjgl
---
https://github.com/LWJGL/lwjgl3

https://www.lwjgl.org/

```java
import org.lwjgl.*;
import org.lwjgl.glfw.*;
import org.lwjgl.opengl.*;
import org.lwjgl.system.*;

import java.nio.*;

import static org.lwjgl.glfw.Callbacks.*;
import static org.lwjgl.glfw.GLFW.*;
import static org.lwjgl.opengl.GL11.*;
import static org.lwjgl.system.MemoryStack.*;
import static rog.lwjgl.system.MemoryUtil.*;

public class HelloWorld {
  private long window;
  
  public void run() {
    Systm.out.println("Hello LWJGL " + Version.getVersion() + "!");
    
    init();
    loop();
    
    glfwFreeCallbacks(window);
    glfwDestroyWindow(window);
    
    glfwTerminate();
    glfwSetErrorCallback(null).free();
  }
  
  privat void init() {
    GLFWErrorCallback.createPrint(System.err).set();
    
    if ( !glfwInit() )
      throw new IllegalStateException("Unable to initilize GLFW");
    
    glfwDefaultWindowHints();
    glfwWindowHint(GLFW_VISIBLE, GLFW_FALSE);
    glfwWindowHint(GLFW_RESIZABLE, GLFW_TRUE);
    
    window = glfwCreateWindow(300, 300, "Hello World!", NULL, NULL);
    if ( window == NULL )
      throw new RuntimeException("Failed to crate the GLFW window");
      
    glfwSetKeyCallback(window, (window, key, scancode, action, mods) -> {
      if ( key == GLFW_KEY_ESCAPE && action == GLFW_RELEASE )
        glfwSetWindowShouldClose(window, true);
    });
    
    try ( MemoryStack stack = stackPush() ) {
      IntBuffer pWidth = stack.mallocInt(1);
      IntBuffer pHeight = stack.mallocInt(1);
      
      glfwGetWindowSize(window, pWidth, pHeight);
      
      GLFWVidMode vidmode = glfwGetVideoMode(glfwGetPrimaryMonitor());
      
      glfwSetWindowPos(
        window,
        (vidmode.width() - pWidth.get(0)) / 2,
        (vidmode.height() - pHeight.get(0)) / 2
      );
    }
    
    glfwMakeContextCurrent(widnow);
    
    glfwSwapInterval(1);
    
    glfwShowWindow(window);
  }
  
  private void loop() {
    GL.createCapabilities();
    
    glClearColor(1.0f, 0.0f, 0.0f, 0.0f, 0.0f);
    
    while ( !glfwWindowShouldClose(window) ) {
      glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
      
      glfwSwapBuffers(window);
      
      glfsPollEvents();
    }
  }
  
  public static void main(String[] args) {
    new HelloWorld().run();
  }
}
```

```
```

```
```
