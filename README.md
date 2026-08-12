### Architecture & How It Works

This is not a standard Streamlit app, even though it looks exactly like one! Because GitHub Pages cannot run a Python server (which Streamlit requires), 
we had to extract the raw HTML. Here is how we built it:

1. The Source file (`app.py`): 
My main portfolio is built in Python/Streamlit and stored in my `KasthuriSathish_Streamlit_Portfolio` repository. 
Inside that app's `app.py`, the entire beautiful User Interface is designed using a massive standard HTML string variable called `html_content.

2. The Extraction (`index.html`):
 To host the website here on GitHub pages without needing Python, we wrote a tiny script called `generate_github_pages.py` in the Streamlit project. When we run that script, it simply copies the raw `html_content` string out of `app.py` and saves it as this standalone `index.html` file.

3. The Resume PDF (The Base64 Trick):
Normally, websites link to a PDF file stored in a folder (like `href="assets/resume.pdf"`). However, Streamlit blocks these kinds of local file downloads. To fix this, we wrote Python code that reads the physical PDF file and translates the entire document into a massive string of random letters and numbers called "Base64". We then pasted that massive string directly inside the HTML button code (`href="data:application/pdf;base64,...”`). 

 Why it works:Because the entire PDF file is mathematically encoded directly inside the HTML button, the browser doesn't even need to search for a file on the internet. When a user clicks "RESUME", the browser instantly decodes the string and downloads the perfectly formatted PDF!

Because the styling (CSS) and the Resume PDF are embedded directly into the code of `index.html`, this single file acts as a completely self-contained website!
