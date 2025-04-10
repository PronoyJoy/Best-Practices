# Best-Practices Of Django && Backend && Others 

--------------------------------------------------------------


# Django - Debug (Feature)
🐍 DEBUG = TRUE OR FALSE 🤔 (DJANGO)

DEBUG = True # development mode (unsafe) 🫥 
DEBUG = False # production mode (safe) 😄 

📚 When DEBUG is set to True it means It will be helpful and will provide 
 detailed information about Errors and other informations which helps us
 to debug or fix the problem , 
🔎 But You must not want them to be in the wrong hand 🐵
 - So if that mistake happens They will be able to retrive environ variables , trace file structure, packages information, hidden routes even views 🦊 

So, The 🐇 Best practise is to set value of DEBUG, using environment variable like If you use django-environ 

--- You need to add some code in Settings.py File 
Import environ
env = environ.Env(DEBUG=(bool, False)) [[[[[🐅 If .env file is missing the value will be False , and you are likely on production where no .env file is exposed.
So ,In production, if .env isn’t there or doesn’t define DEBUG, it will automatically be False thanks to that default. ]]]]]

environ.Env.read_env() [[reading debug value from .env file ]] which is set to True in .env file like we store the secret keys and others in .env file as I wrote before ....

DEBUG = env('DEBUG') [setting the value in settings.py]


Another Block You can add for ensuring debug :
“When I’m in production, activate all the security settings I’ve written below.”

if not DEBUG:
 ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']
🔐 Why?
 Django blocks requests that don’t match this list to prevent host header attacks.

 # Redirect all HTTP traffic to HTTPS
 SECURE_SSL_REDIRECT = True
 🔐 Why?
 Redirects all HTTP traffic to HTTPS.

 # Set secure cookies
 SESSION_COOKIE_SECURE = True 🔐 Why?
 Tells browsers to only send the session cookie over HTTPS

 CSRF_COOKIE_SECURE = True 🔐 Why?
 Same idea — protects the CSRF token cookie from being sent over insecure HTTP.

 # Enable HTTP Strict Transport Security (HSTS)
 SECURE_HSTS_SECONDS = 31536000 # 1 year in seconds
🛡️ Why?
 This enables HTTP Strict Transport Security (HSTS), telling browsers:
"Only connect to me using HTTPS for the next year."
Prevents downgrade attacks and cookie hijacking.

 SECURE_HSTS_INCLUDE_SUBDOMAINS = True
🔐 Why?
 Same idea — protects the CSRF token cookie from being sent over insecure HTTP.

 SECURE_HSTS_PRELOAD = True

 # Protect against content sniffing and XSS
 SECURE_CONTENT_TYPE_NOSNIFF = True
🛡️ Why?
 Prevents browsers from guessing file types (which can lead to XSS attacks).
 For example, a .txt file pretending to be a .html.

 SECURE_BROWSER_XSS_FILTER = True
🛡️ Why?
 Prevents browsers from guessing file types (which can lead to XSS attacks).
 For example, a .txt file pretending to be a .html.

 # Prevent clickjacking
 X_FRAME_OPTIONS = 'DENY'
🧱 Why?
 Prevents your site from being embedded in an <iframe> on another site.
 This protects against clickjacking attacks.
