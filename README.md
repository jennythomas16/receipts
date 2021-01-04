Information Extraction from Scanned Receipts: 
The aim of this task was to extract texts from given receipts, and save the texts for each receipt image in a json file.


    Step 1: OCR, Text Region Detection : Extracting all the text from given Invoice Image
    Step 2: using Bi-directional LSTM based approach, Recognising Key information from the text.

For step two we have used Tesseract OCR: Tesseract, the most common and high-quality OCR library, is an optical character recognition engine with open source code. For text search and recognition of images, OCR uses artificial intelligence. In pixels, letters, words and sentences, Tesseract seeks models.

For step two we have used Bi-directional LSTM, The BRNN theory is to divide the neurons of a normal RNN into two ways, one for the positive direction of time (forward states), and one for the negative direction of time (backward states). The output of those two states is not related to inputs from states in the opposite direction.

1.Importing all the required libraries
		
		import os
		import cv2
		from PIL import Image
		from PIL import ImageDraw
		import pytesseract
		import easyocr
		import json

	
i. Python's OS module includes functions to communicate with the operating system. OS, is available under the basic utility modules of Python.
ii. Python's OpenCV Module is a Python library designed to  solve and simplify computer vision problems.
iii. Python's PIL or Pillow Module is a Python Imaging Library (PIL), which provides support for images to be opened, manipulated and saved.
iv. Python's pytesseract Module is an Open Source Text Recognition (OCR) Engine, Tesseract is available under the Apache 2.0 license. It can be used to extract printed text from images directly or (for programmers) using an API.
v. Python's easyocr Module is a python package that makes it possible to convert an image to text. It is the simplest way to implement OCR by far.
vi. Python's json Module is the JavaScript Object Notation (JSON) that is widely used structured format for transferring information as text.


2.provide path for all the receipts
			
			path='C:/Users/jenny/Desktop/test'
			mypiclist=os.listdir(path)

3.Creatting a for loop to get all the data from the images 
		
			for j,y in enumerate(mypiclist):
    	img=cv2.imread(path + "/"+y)
   	 #img = PIL.Image.open("C:/Users/jenny/Desktop/test/T1.jpg")
    	#cv2.imshow(y,img)
    	#cv2.waitKey(1000)
    	#cv2.destroyAllWindows() 
    	bounds = reader.readtext(img)
    	def draw_boxes(image, bounds, color='yellow', width=2):
        	draw = ImageDraw.Draw(image)
        	for bound in bounds:
           	 p0, p1, p2, p3 = bound[0]
           	 draw.line([*p0, *p1, *p2, *p3, *p0], fill=color, width=width)
           	 return image
4.Creating JSon files in a loop to write and store the data into.
		
    	filename = y
    	with open(y.json, 'w') as f:
							#f.write(i[1])
            	json.dump(i[1], f)
            	print(filename.json)
