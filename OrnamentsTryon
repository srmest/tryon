package rectpoly;

import com.googlecode.javacv.CanvasFrame;
import com.googlecode.javacv.FrameGrabber;
import com.googlecode.javacv.OpenCVFrameGrabber;
import com.googlecode.javacv.cpp.opencv_core.CvMemStorage;
import com.googlecode.javacv.cpp.opencv_core.CvPoint;
import com.googlecode.javacv.cpp.opencv_core.CvRect;
import com.googlecode.javacv.cpp.opencv_core.CvScalar;
import com.googlecode.javacv.cpp.opencv_core.CvSeq;
import com.googlecode.javacv.cpp.opencv_core.IplImage;
import com.googlecode.javacv.cpp.opencv_objdetect.CvHaarClassifierCascade;


import static com.googlecode.javacv.cpp.opencv_core.*;
import static com.googlecode.javacv.cpp.opencv_objdetect.*;

public class demo_necklace_polygon{
	public static final String XML_FILE = 
			"haarcascade_frontalface_alt.xml";
	static IplImage img;
	static IplImage frame;
	static CvRect neck;
//	CvSize Out_Img_size;
	
	public static void main(String[] args) {
		//Create canvas frame for displaying webcam.
	     CanvasFrame canvas = new CanvasFrame("Webcam");
	      
	   
	  //Set Canvas frame to close on exit
	     canvas.setDefaultCloseOperation(javax.swing.JFrame.EXIT_ON_CLOSE);   
	      
	     //Declare FrameGrabber to import output from webcam
	     FrameGrabber grabber = new OpenCVFrameGrabber("");  
	      
	      
	     try {      
	       
	      //Start grabber to capture video
	      grabber.start();      
	       
	         
	      while (true) {
	        
	       //inser grabed video fram to IplImage img
	       img = grabber.grab();
	        
	       //Set canvas size as per dimentions of video frame.
	       canvas.setCanvasSize(grabber.getImageWidth(), grabber.getImageHeight()); 
	        
	       if (img != null) {      
	         //Flip image horizontally
	         cvFlip(img, img, 1);
	        //Show video frame in canvas
//	        int count = 0;   
//	        while(count==0);
			CvHaarClassifierCascade cascade = new 
				CvHaarClassifierCascade(cvLoad(XML_FILE));
		CvMemStorage storage = CvMemStorage.create();
		CvSeq sign = cvHaarDetectObjects(
				img,
				cascade,
				storage,
				1.5,
				3,
				CV_HAAR_DO_CANNY_PRUNING);
 
		cvClearMemStorage(storage);
 
		int total_Faces = sign.total();		
 
		for(int i = 0; i < total_Faces; i++)
		{
			CvRect r = new CvRect(cvGetSeqElem(sign, i));
			cvRectangle (
					img,
					cvPoint(r.x(), r.y()),
					cvPoint(r.width() + r.x(), r.height() + r.y()),
					CvScalar.RED,
					2,
					CV_AA,
					0);			
	   
		
		/*frame = cvCreateImage(cvGetSize(img),8,1);
		cvAbsDiff( 
		          frame,
                  img,img,3
                 );*/
			
		double neckX;
		double neckY;
		double neckHeight;
		double neckWidth;
		
		neckX = (r.x() - 1.25);
		neckY = (r.y() + r.height()+12);
        
		neckHeight = r.height() + 2;
		neckWidth = r.width() ;
		/*System.out.println("neckX : "+neckX);
		System.out.println("neckY : "+neckY);
		System.out.println("neckH : "+neckHeight);
		System.out.println("neckW : "+neckWidth);*/
		
		int x= Double.valueOf(neckX).intValue();
		int y=Double.valueOf(neckY).intValue();
		int h=Double.valueOf(neckHeight).intValue();
		int w=Double.valueOf(neckWidth).intValue();   
		
		neck = new CvRect(x,y,w,h);
		System.out.println("n: "+ neck.width());
		cvRectangle (
				img,
				cvPoint(neck.x(), neck.y()),
				cvPoint(neck.width() + neck.x(), neck.height() + neck.y()),
				CvScalar.GREEN,
				2,
				CV_AA,
				0);	
		
		   CvPoint hatPoints = new CvPoint(3);
		   /*hatPoints.position(0).x(r.x()-r.width()/10);
		   hatPoints.y(r.y()+r.height()*1);
		   hatPoints.position(1).x(r.x()+r.width()*11/10);
		   hatPoints.y(r.y()+r.height()*1);
		   hatPoints.position(2).x(r.x()-r.width()/2);
		   hatPoints.y(r.y()+r.height()*2); */
		   
		   hatPoints.position(0).x(x);      hatPoints.y(y);
		   hatPoints.position(1).x(x+w);    hatPoints.y(y);
		   hatPoints.position(2).x(x+w/2);  hatPoints.y(y+h);
		   
		cvFillConvexPoly(img, hatPoints.position(0), 3, CvScalar.BLUE, CV_AA, 0);
		
		}
		
		canvas.showImage(img); 
		cvClearMemStorage(storage);
	       }
	      }}
	      catch (Exception e) {
		    	 e.printStackTrace();
		     }
	}}
		 
		
