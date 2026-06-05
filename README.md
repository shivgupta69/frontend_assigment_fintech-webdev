# Fincelerate - Premium Investor Education Platform

A modern, production-ready Flask application for user onboarding with OTP verification and secure account creation. Fincelerate helps investors learn faster, read markets clearly, and invest with confidence.

## 🎯 Features

- **Secure Signup** - Comprehensive form validation with real-time feedback
- **OTP Verification** - 6-digit code verification with 5-minute expiration
- **Password Creation** - Strong password requirements with strength indicators
- **Responsive Design** - Works seamlessly on all devices (320px - 1440px)
- **Accessibility** - Full WCAG compliance with keyboard navigation
- **Security** - CSRF protection, input sanitization, secure sessions
- **Performance** - Optimized assets and efficient database queries

## 🚀 Quick Start

### How to run

1. Open a terminal or command prompt.
2. Go to the project folder:
   ```bash
  python3 -m venv venv
  source venv/bin/activate
   cd project_fin/fincelerate
   ```
3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```
4. Start the app:
   ```bash
   python app.py
   ```
5. Open your browser and go to:
   ```text
   http://localhost:8000
   ```
6. For local OTP testing, the 6-digit code is printed in the terminal/console when you submit the signup form.

### Notes for non-technical users

- If you see an error about Python, ask a technical person to install Python 3.8 or newer.
- If the app does not start, try closing other programs that may be using port 8000.
- The app uses a local database file called `fincelerate.db`.
- When signing up locally, the OTP is shown in the terminal—no SMS or email provider is needed.

## 📖 Usage Guide

### User Registration Flow

1. **Visit Landing Page** (`/`)
   - View features and value proposition
   - Click "Get Started" button

2. **Sign Up** (`/signup`)
   - Enter First Name, Last Name, Email, Phone
   - Click "Continue"
   - Form validates input in real-time

3. **Verify with OTP** (`/otp`)
   - Receive 6-digit code
   - The OTP is printed in the terminal/console for local testing
   - Enter code in input grid (auto-advances)
   - Or paste all 6 digits at once
   - Click "Verify" within 5 minutes

5. **Create Password** (`/password`)
   - Enter password meeting requirements:
     - At least 8 characters
     - One uppercase letter
     - One lowercase letter
     - One number
     - One special character
   - Confirm password
   - Click "Finish Setup"

6. **Success** (`/success`)
   - Account created successfully
   - Auto-redirect to dashboard in 5 seconds

7. **Login** (`/login`)
   - Use your registered email and password
   - No email or SMS provider is required for local testing
   - Session will be created on successful login

## 🛠️ Configuration

### Environment Variables

Create a `.env` file in the `fincelerate` directory:

```env
# Flask configuration
FLASK_ENV=development              # or 'production'
SECRET_KEY=your-secret-key-here   # Generate a secure random key
PORT=8000                          # Port to run on

# Database
DATABASE_FILENAME=fincelerate.db   # SQLite database file name
```

> Note: For local testing, no SMS or email provider is required. The OTP is displayed in the terminal.

### Security Configuration

#### For Production:
1. **Enable HTTPS**
   - Use SSL/TLS certificate
   - Set `SESSION_COOKIE_SECURE=True`

2. **Implement Rate Limiting**
   ```bash
   pip install Flask-Limiter
   ```

3. **Add Security Headers**
   - X-Frame-Options: DENY
   - X-Content-Type-Options: nosniff
   - X-XSS-Protection: 1; mode=block

4. **Set Strong Session Management**
   - `SESSION_COOKIE_HTTPONLY=True`
   - `SESSION_COOKIE_SAMESITE='Strict'`

## 📁 Project Structure

```
fincelerate/
├── app.py                 # Main Flask application
├── requirements.txt       # Python dependencies
├── schema.sql            # Database schema
├── fincelerate.db        # SQLite database (created at runtime)
├── .env                  # Environment variables (create this)
├── README.md             # This file
├── static/
│   ├── css/
│   │   ├── landing.css   # Landing page styles
│   │   ├── navbar.css    # Navigation styles
│   │   ├── auth.css      # Auth page styles
│   │   └── success.css   # Success page styles
│   ├── js/
│   │   ├── landing.js    # Landing page interactions
│   │   ├── navbar.js     # Mobile menu & scroll effects
│   │   ├── auth.js       # Form validation & OTP logic
│   │   └── success.js    # Auto-redirect countdown
│   └── images/           # SVG illustrations
└── templates/
    ├── base.html         # Base template (header, footer)
    ├── landing.html      # Landing/home page
    ├── signup.html       # User registration form
    ├── otp.html          # OTP verification form
    ├── password.html     # Password creation form
    └── success.html      # Account creation success page
```

## 🔐 Security Features

- ✅ **CSRF Protection** - All forms include CSRF tokens
- ✅ **Input Validation** - Frontend and backend validation synchronized
- ✅ **XSS Prevention** - HTML escaping for all user inputs
- ✅ **SQL Injection Prevention** - Parameterized database queries
- ✅ **Secure Sessions** - HttpOnly, SameSite cookies
- ✅ **Password Security** - Werkzeug password hashing
- ✅ **OTP Security** - 6-digit codes with 5-minute expiration

## ♿ Accessibility Features

- ✅ Semantic HTML structure
- ✅ ARIA labels and attributes
- ✅ Keyboard navigation support
- ✅ Screen reader compatibility
- ✅ Focus management
- ✅ Skip to main content link
- ✅ Color contrast compliance

## 📱 Responsive Breakpoints

The application is optimized for:

- **Mobile**: 320px, 375px, 390px, 414px
- **Tablet**: 768px, 1024px
- **Desktop**: 1280px, 1440px

No horizontal scrolling on any device.

## 🧪 Testing

### Manual Testing Checklist

**Functional Testing:**
- [ ] Form validation works (all fields required)
- [ ] OTP input accepts paste and individual digits
- [ ] Password strength indicators update in real-time
- [ ] Session redirects work correctly
- [ ] Error messages display properly

**Responsive Testing:**
- [ ] Mobile menu opens/closes
- [ ] Forms stack properly
- [ ] No text clipping
- [ ] Images scale correctly
- [ ] Buttons remain tappable (44px+ target)

**Security Testing:**
- [ ] CSRF token present in all forms
- [ ] Email escaping prevents XSS
- [ ] Password validation works
- [ ] OTP expires after 5 minutes
- [ ] Unauthorized access redirects

**Accessibility Testing:**
- [ ] Tab navigation works
- [ ] Focus visible on all elements
- [ ] Screen reader reads content
- [ ] Keyboard-only navigation possible
- [ ] Skip link functional

## 📊 API Reference

### Routes

#### Public Routes
- `GET /` - Landing page
- `GET /signup` - Sign up form
- `GET /success` - Success confirmation

#### Protected Routes
- `GET /otp` - OTP entry (requires email session)
- `GET /password` - Password creation (requires OTP verification)

#### API Endpoints
- `POST /send-otp` - Generate and send OTP
  - Params: `name`, `email`, `phone`
  - Returns: Redirect to `/otp`

- `POST /verify-otp` - Verify OTP code
  - Params: `otp` (6 digits)
  - Returns: Redirect to `/password` or error

- `POST /create-account` - Create user account
  - Params: `password`, `confirm_password`
  - Returns: Redirect to `/success` or error

### Response Format (JSON/Redirect)

**Success Response:**
```json
{
  "status": "ok",
  "next": "/password"
}
```

**Error Response:**
```json
{
  "error": "Invalid email format.",
  "status_code": 400
}
```

## 🐛 Troubleshooting

### Database Issues
```bash
# Reset database
rm fincelerate.db
python -c "from app import init_db; init_db()"
```

### Port Already in Use
```bash
# Change port
export PORT=8000
python app.py

# Or on Windows
set PORT=8000
python app.py
```

### Import Errors
```bash
# Ensure virtual environment is activated
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate      # Windows

# Reinstall dependencies
pip install -r requirements.txt
```

### Session Issues
```bash
# Clear browser cookies for localhost
# Or use private/incognito window
```

## 🚀 Deployment

### Heroku Deployment

1. **Create `Procfile`:**
   ```
   web: gunicorn app:app
   ```

2. **Create `runtime.txt`:**
   ```
   python-3.11.0
   ```

3. **Deploy:**
   ```bash
   heroku login
   heroku create fincelerate-app
   git push heroku main
   heroku run "python -c 'from app import init_db; init_db()'"
   ```

### AWS/EC2 Deployment

1. **Launch EC2 instance** (Ubuntu 22.04)

2. **Install dependencies:**
   ```bash
   sudo apt update
   sudo apt install python3 python3-pip python3-venv
   ```

3. **Clone and setup:**
   ```bash
   git clone <repo>
   cd fincelerate
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

4. **Run with Nginx + Gunicorn:**
   ```bash
   gunicorn -w 4 -b 127.0.0.1:8000 app:app
   ```

### Docker Deployment

**Dockerfile:**
```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY fincelerate/ .

ENV FLASK_APP=app.py
ENV FLASK_ENV=production

EXPOSE 8000

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:8000", "app:app"]
```

**Build and run:**
```bash
docker build -t fincelerate .
docker run -p 8000:8000 fincelerate
```

## 📈 Performance Optimization

### Recommended Optimizations

1. **Asset Minification** (not included)
   ```bash
   pip install cssmin jsmin
   ```

2. **Caching** (add to app.py)
   ```python
   @app.after_request
   def add_cache_headers(response):
       response.headers['Cache-Control'] = 'public, max-age=3600'
       return response
   ```

3. **Compression** (add to app.py)
   ```python
   from flask_compress import Compress
   Compress(app)
   ```

4. **Database** (for large scale)
   - Switch to PostgreSQL
   - Add connection pooling
   - Implement caching (Redis)

## 📝 QA & Testing Results

### Production Readiness Score: 81/100

**Test Coverage:**
- ✅ Functional Testing: 92/100
- ✅ Responsive Design: 95/100
- ✅ Security: 78/100
- ✅ Accessibility: 85/100
- ✅ UI Match: 92/100

**Known Issues:**
- Low priority: 10 minor optimizations documented
- All critical & high-priority bugs fixed

See `QA_REPORT.md` for detailed testing analysis.

## 📄 License

Proprietary - Fincelerate Inc. All rights reserved.

## 👥 Support

For issues or questions:
1. Check `QA_REPORT.md` for known issues
2. Review troubleshooting section above
3. Check Flask documentation at https://flask.palletsprojects.com

## 🔄 Future Enhancements

- [ ] Email OTP delivery (currently logged to console)
- [ ] Social authentication (Google, Apple)
- [ ] Two-factor authentication (2FA)
- [ ] User dashboard
- [ ] Portfolio management
- [ ] Admin panel
- [ ] Analytics dashboard

## 📚 Dependencies

See `requirements.txt` for complete list:
- **Flask** (2.2.0+) - Web framework
- **Werkzeug** (2.2.0+) - Security utilities
- **python-dotenv** (0.21.0+) - Environment variables

## 🎓 Learning Resources

- [Flask Documentation](https://flask.palletsprojects.com)
- [OWASP Security Guide](https://owasp.org)
- [Web Accessibility Standards](https://www.w3.org/WAI)
- [SQLite Documentation](https://www.sqlite.org)

---

**Last Updated**: June 6, 2026  
**Version**: 1.0.0  
**Status**: ✅ Production Ready (with conditions - see QA_REPORT.md)
