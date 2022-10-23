It looks simple but retrieving openGl pixel values from datatype `unsigned int *pixel` took me some time to figur out.
Maybe i had a bad programming day..?

How to get pixel values from this?

      unsigned int *pixels = new unsigned int[size];

Example:

      //! Color channels Rgba=4.
      int channels=4;
      //! The screen width in pixels.
      int width=200;
      //! The screen height in pixels.
      int height=200;
      //! Needed memory size.
      int size=channels*width*height;
      //! Create pixel storage for a certain size.
      GLubyte *pixels = new GLubyte[size];
      if(pixels){
        //! OpenGl function to read a rectangular of the screen pixels.
        glReadPixels(0, 0, width, height, GL_RGBA, GL_UNSIGNED_BYTE, pixels);
      }
      //! Look for pixel value at:
      int x=5;
      int y=5;
      //! Check screen limits.
      if( x < 0 || x > width -1 || y < 0 || y > height -1 ){
        //! Out of reach.
      } else {
        //! Idx is the pixel counter.
        int idx = (y * width + x) * channels;
        //! Pixel color output.
        GLubyte r = pixels[ idx + 0 ];
        GLubyte g = pixels[ idx + 1 ];
        GLubyte b = pixels[ idx + 2 ];
        GLubyte a = pixels[ idx + 3 ];
        //! Print result.
        std::cout<<"r:"<<(GLint)r<<" g:"<<(GLint)g<<" b:"<<(GLint)b<<" a:"<<(GLint)a<<std::endl;
      }
      
My terminal output was :

    r:128 g:128 b:128 a:128
    
The values should be in the range 0-255.    
                
