# CS-5330 Final Project: ISBN Scanner  

### Team Members  
1. **Atiq Sohail Mohammed** - [mohammed.at@northeastern.edu](mailto:mohammed.at@northeastern.edu)  
2. **Sricharan R Iyengar** - [iyengar.sr@northeastern.edu](mailto:iyengar.sr@northeastern.edu)  

---

## Project Overview  

The **ISBN Scanner** is an intuitive desktop application designed to streamline the process of ISBN (International Standard Book Number) recognition and book information retrieval. This application serves as a practical tool for librarians, bookstore owners, book collectors, and anyone needing quick access to book details through barcode scanning.

### Purpose

This project was developed as part of the CS-5330 (Pattern Recognition & Computer Vision) course to demonstrate practical applications of computer vision techniques in real-world scenarios. The application combines image processing, barcode detection, and API integration to create a seamless user experience for book identification.

---

## Key Features

The ISBN Scanner offers three distinct modes of operation to accommodate various use cases:

### 1. **Video-Based Scanning**
- Real-time ISBN detection using webcam
- Continuous scanning with automatic ISBN recognition
- Multiple books can be scanned in a single session
- Inactivity detection (alerts after 15 seconds of no detection)
- Control panel for managing scanning sessions
- Automatic duplicate ISBN filtering

### 2. **Image-Based Scanning**
- Upload and scan ISBN from static images
- Advanced image processing for barcode extraction
- Supports multiple image formats (JPG, JPEG, PNG, BMP, TIFF)
- Gradient-based edge detection using Sobel operators
- Morphological operations for barcode region enhancement
- Automated barcode region cropping and upscaling

### 3. **Manual Entry**
- Direct ISBN input through keyboard
- Useful for damaged or unreadable barcodes
- Quick lookup without camera or image files

### Book Information Retrieval
- Automatic book metadata fetching using OpenLibrary API
- Displays book title and authors
- Fallback to web-based ISBN search when metadata unavailable
- Integration with isbnsearch.org for comprehensive book details

---

## Technical Architecture

### Core Components

1. **scanner_gui.py** - Main application entry point and GUI framework
   - Built with Tkinter for cross-platform compatibility
   - Clean, user-friendly interface design
   - Button-based navigation for three scanning modes

2. **scan_video.py** - Real-time video scanning module
   - OpenCV integration for webcam access
   - Threading for non-blocking video processing
   - pyzbar for EAN13 barcode decoding
   - Session management with control panel

3. **scan_image.py** - Image processing and analysis module
   - Advanced computer vision techniques for barcode detection
   - Scharr gradient computation for edge detection
   - Morphological transformations for noise reduction
   - Contour detection and bounding box extraction
   - Image upscaling using Lanczos interpolation

4. **manual_entry.py** - Manual ISBN input handler
   - Simple dialog-based ISBN entry
   - Validation and metadata retrieval

5. **isbn_utils.py** - Utility functions for ISBN processing
   - API integration with OpenLibrary (isbnlib)
   - Book metadata extraction
   - Error handling and fallback mechanisms

### Technologies & Libraries

- **Python 3.12+** - Core programming language
- **OpenCV (cv2)** - Computer vision and image processing
- **pyzbar** - Barcode detection and decoding
- **isbnlib** - ISBN validation and metadata retrieval
- **Tkinter** - GUI framework
- **imutils** - OpenCV convenience functions
- **NumPy** - Numerical operations and array manipulation
- **threading** - Concurrent video processing
- **webbrowser** - Fallback web-based book search

### Computer Vision Techniques

The application employs several advanced image processing techniques:

1. **Gradient Computation**: Sobel operators calculate directional gradients
2. **Gradient Subtraction**: X-gradient minus Y-gradient highlights horizontal patterns (typical in barcodes)
3. **Gaussian Blur**: Reduces noise while preserving edges
4. **Thresholding**: Binary image creation for contour detection
5. **Morphological Operations**: Closing, erosion, and dilation to enhance barcode regions
6. **Contour Analysis**: Identification of largest connected components
7. **Rotated Bounding Box**: Handles barcodes at various angles
8. **Region Scaling**: Dynamic adjustment for optimal barcode detection
9. **Super-Resolution**: Image upscaling for improved decoding accuracy

---

## System Requirements  

### For Running Pre-built Executable
- **Operating System**: Windows 10 or Windows 11  
- **No additional software required**

### For Running from Source
- **Operating System**: Windows, macOS, or Linux
- **Python**: Version 3.12 or above
- **Webcam**: Required for video-based scanning
- **Internet Connection**: Required for fetching book metadata

---

## Installation & Setup

### Option 1: Using Pre-built Executable (Windows Only)

1. **Download the Application**  
   - Download the latest release of **ISBN_Scanner v1.01** from the repository

2. **Extract the Archive**  
   - Use WinRAR, 7Zip, or Windows built-in extractor

3. **Navigate to Application Directory**  
   - Open the extracted folder **ISBN_Scanner v1.01**

4. **Launch the Application**  
   - Double-click on **scanner_gui.exe**

### Option 2: Running from Source Code

1. **Clone the Repository**
   ```bash
   git clone https://github.com/atiq-sm/CS-5330-Final-Project.git
   cd CS-5330-Final-Project
   ```

2. **Install Required Dependencies**
   ```bash
   pip install opencv-python pyzbar isbnlib imutils numpy
   ```

3. **Run the Application**
   ```bash
   python scanner_gui.py
   ```

---

## Usage Guide

### Video Scanning Workflow

1. Click **"Scan from Video"** button
2. Allow webcam access if prompted
3. Position book barcode in front of camera
4. Application automatically detects and displays ISBN
5. Continue scanning additional books
6. Click **"Done Scanning"** in control panel when finished
7. View summary of all scanned books with details

**Tips for Video Scanning:**
- Ensure good lighting conditions
- Hold barcode steady and parallel to camera
- Maintain distance of 6-12 inches from camera
- If no detection after 15 seconds, system prompts continuation

### Image Scanning Workflow

1. Click **"Scan from Image"** button
2. Select image file containing ISBN barcode
3. Application processes image and extracts ISBN
4. Book details displayed automatically
5. Repeat for additional images

**Tips for Image Scanning:**
- Use high-resolution images for best results
- Ensure barcode is clearly visible
- Avoid excessive shadows or reflections
- Supported formats: JPG, JPEG, PNG, BMP, TIFF

### Manual Entry Workflow

1. Click **"Manual Entry"** button
2. Enter 13-digit ISBN in dialog box
3. Click OK to fetch book details
4. Information displayed or web page opens

---

## Workflow Diagram  

Below is a visual representation of the application's workflow:  
![Application Workflow Diagram](https://github.com/user-attachments/assets/d98bf26d-c4d3-41d5-92ff-ab28498f34e4)  

---

## Project Structure

```
CS-5330-Final-Project/
├── scanner_gui.py          # Main application GUI
├── scan_video.py           # Video scanning module
├── scan_image.py           # Image scanning module
├── manual_entry.py         # Manual ISBN entry
├── isbn_utils.py           # ISBN utility functions
├── Images/                 # Sample images for testing
│   ├── Img1 (1).jpg
│   ├── Img2.jpg
│   └── Img3.jpg
├── README.md               # Project documentation
├── CS 5330.pptx           # Project presentation
└── ISBN_Scanner v1.01.zip # Packaged executable
```

---

## Development Workflow

### Building from Source

The application can be packaged into a standalone executable using PyInstaller:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed scanner_gui.py
```

### Testing

Test the application with the provided sample images in the `Images/` directory:
- Various barcode orientations
- Different image qualities
- Multiple lighting conditions

---

## Known Limitations

- Video scanning requires adequate lighting for optimal detection
- Some ISBN formats (ISBN-10) may require conversion to ISBN-13
- Internet connection required for metadata retrieval
- Image scanning performance depends on image quality
- Windows executable only compatible with Windows 10/11

---

## Future Enhancements

Potential improvements for future versions:

1. **Batch Processing**: Scan multiple images in a single operation
2. **Database Integration**: Store scanned book history locally
3. **Export Functionality**: Generate CSV/Excel reports of scanned books
4. **Multi-language Support**: Internationalization for global users
5. **Mobile Version**: Android/iOS companion apps
6. **Advanced Analytics**: Statistics on scanned books and collections
7. **ISBN-10 Support**: Direct handling of older ISBN format
8. **OCR Integration**: Fallback text recognition when barcode detection fails
9. **Cloud Sync**: Backup and sync across devices
10. **Barcode Generation**: Create ISBN barcodes for custom entries

---

## Course Context

This project was developed for **CS-5330: Pattern Recognition & Computer Vision** at Northeastern University. It demonstrates practical applications of computer vision concepts including:

- Edge detection and gradient analysis
- Morphological image processing
- Contour detection and analysis
- Real-time video processing
- Feature extraction from images
- Integration of CV techniques in user-facing applications

---

## Acknowledgments

- **pyzbar**: Open-source barcode detection library
- **OpenLibrary**: Free book metadata API
- **OpenCV**: Comprehensive computer vision library
- **isbnlib**: Python library for ISBN validation and metadata

---

- **GitHub Issues**: Please open an issue in the repository for bug reports or feature requests

---

## License

This project was created for educational purposes as part of coursework at Northeastern University.

--- 
