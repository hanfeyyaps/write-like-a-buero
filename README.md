**Write Like a Bureaucrat App (IM2025)**

The 'Write Like a Bureaucrat App' is designed in line with Innovation Month 2025 to transform text provided by users into a formal, bureaucratic style, specifically adhering to the Australian Government Style Manual. It leverages a Retrieval Augmented Generation (RAG) architecture, grounding its AI responses to the official style guide to ensure accurate and relevant transformations, enhancing contextual relevant to the style guide. Users can specify their target audience and desired output format (e.g., email, report), and the app provides clear explanations of all changes made. This bot perfectly embodies the "Build a Bureaucrat Bot" challenge by automating the often routine task of formal communication, promoting adherence to established guidelines, and streamlining the creation of precise and formatted documentation.  


**Features**

Content Transformation: Rewrites user-provided text into a formal, bureaucratic style based on the Australian Style Manual.

Audience and Format Selection: Allows users to specify the target audience (e.g., General Public, Senior Executives) and output format (e.g., Article, Email, Brief, Report) for tailored output.

Explanation of Changes: Provides a clear, itemized explanation of the specific stylistic, grammatical, and spelling changes made, including "Before" and "After" examples, and references to the relevant Australian Style Manual guidelines (with URLs).

Australian English Adherence: Ensures all transformations and explanations use Australian English spelling, grammar, and phrasing.

RAG-Grounded Responses: Utilizes Retrieval Augmented Generation (RAG) to ensure the AI's advice is directly informed by the Australian Style Manual's content, reducing hallucinations and increasing accuracy.

**Technologies Used**

**Frontend**
HTML5: Structure of the web application.

CSS (Tailwind CSS): For responsive and modern styling.

JavaScript (ES6+): Handles user interactions, API calls, and dynamic content rendering.

**Backend (Python Flask)**
Python 3.x: Core programming language.

Flask: A lightweight web framework for the backend API.

Flask-CORS: Enables Cross-Origin Resource Sharing for frontend-backend communication.

Requests: For making HTTP requests to external APIs (e.g., Gemini API for embeddings).

BeautifulSoup4: For web scraping the Australian Style Manual content.

NumPy: For numerical operations, particularly with embeddings.

Google Cloud Vertex AI Client Libraries: For interacting with Vertex AI Vector Search (for RAG) and potentially other Vertex AI services.

**AI/Cloud Services**
Google Gemini API (gemini-2.0-flash): Used for text generation (content transformation and explanation).

Google Gemini API (text-embedding-004): Used for generating vector embeddings of text content.

Google Cloud Storage: For storing raw scraped data and processed embeddings.

Google Cloud Vertex AI Vector Search: For efficient semantic search and retrieval of relevant style manual chunks (the RAG component).

Google Cloud Run: Serverless platform for deploying the Python Flask backend.

Firebase Hosting: For hosting the static frontend web application.

**Architecture Overview**
The application follows a client-server architecture with a RAG component:

Frontend (HTML/JS): The user interface where users input text and select options. It sends requests to the Flask backend for content retrieval and directly to the Gemini API for text generation.

Backend (Python Flask on Cloud Run):

Receives user queries from the frontend.

Generates embeddings for the user query using the text-embedding-004 model.

Queries a Vertex AI Vector Search index (pre-populated with embeddings of the Australian Style Manual) to retrieve the most semantically relevant sections of the manual.

Returns the retrieved content (text, URL, title) to the frontend.

RAG Process: The frontend then constructs an "augmented prompt" by combining the user's original text with the relevant style manual guidelines retrieved from the backend.

LLM Interaction (Gemini API): This augmented prompt is sent to the gemini-2.0-flash model via the Gemini API. The LLM generates the transformed content and a structured JSON explanation of changes, leveraging the provided context.

Output Display: The frontend receives and displays the transformed content and dynamically renders the explanation, including clickable links to the original style manual sources.

**Setup and Installation**
This project involves setting up both a Python backend and a static HTML/JavaScript frontend.

1. Backend Setup (Python Flask)
The backend handles the RAG retrieval process.

**Prerequisites:**
Python 3.8+ installed.

pip (Python package installer).

Google Cloud Project with billing enabled.

Vertex AI API and Cloud Storage API enabled in your GCP project.

A Vertex AI Vector Search index populated with the Australian Style Manual content (refer to the model-grounding-guide and process-scraped-content-guide for detailed steps on web scraping, embedding generation, and index creation).

**Steps:**
Clone the Repository (or create files):
If you have a backend repository, clone it. Otherwise, create a directory for your backend and place app.py, requirements.txt, and Dockerfile within it.

Install Dependencies:
Navigate to your backend directory in the terminal and install the required Python packages:

pip install -r requirements.txt

**Set Environment Variables:**
Your app.py should read sensitive information from environment variables.

GEMINI_API_KEY: Your Gemini API key for embeddings.

GCP_PROJECT_ID: Your Google Cloud Project ID.

GCP_REGION: The region where your Vertex AI Vector Search index is deployed (e.g., us-central1).

INDEX_ENDPOINT_ID: The ID of your deployed Vertex AI Vector Search index endpoint.

For local testing, you can set these in your terminal (for a single session):

export GEMINI_API_KEY="YOUR_API_KEY"
export GCP_PROJECT_ID="your-project-id"
export GCP_REGION="us-central1"
export INDEX_ENDPOINT_ID="your-index-endpoint-id"

For production deployment on Cloud Run, these will be set during the gcloud run deploy command.

**Usage**
Enter Your Content: Type or paste the text you want to transform into the "Your Content" textarea.

Author Name (Optional): Provide an author name if desired, which can be used in some output formats (e.g., reports, articles).

Select Target Audience: Choose the intended audience for the transformed content from the dropdown (e.g., General Public, Senior Executives).

Select Output Format: Choose the desired output document format from the dropdown (e.g., Article, Email, Brief, Report).

Apply Style: Click the "Apply Australian Style Manual" button.

View Output: The "Output" section will display the transformed text, and the "Explanation of Changes" section will detail the modifications made, linking back to the relevant style manual guidelines.

**Deployment**
The application is designed for deployment on Google Cloud Platform:

Backend: Deployed as a containerized service on Google Cloud Run for serverless, scalable hosting. Refer to the google-cloud-deployment-guide for detailed deployment steps, including Dockerfile creation, image building, and service deployment.

Frontend: Can be hosted on Firebase Hosting, GitHub Pages, Netlify, or Vercel as a static site. Firebase Hosting is recommended for seamless integration with other Google Cloud services.

**Contributing**
Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please feel free to:

Open an issue to discuss proposed changes.

Submit a pull request with your enhancements.

**Contact**
For questions or feedback, please connect with Han Fey Yap on LinkedIn.
