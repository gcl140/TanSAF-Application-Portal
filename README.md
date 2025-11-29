# TanSAF Application Portal

A comprehensive Django-based web application for managing scholarship applications for the Tanzania Scholars Alumni Foundation (TanSAF). The portal enables prospective scholars to submit applications for cohort and internship programs through a structured multi-step process.

## 🌟 Features

### For Applicants
- **User Registration & Authentication** - Secure email-based account activation with password management
- **Multi-Step Application Forms** - Guided application process with progress tracking
- **Two Application Tracks**:
  - **Cohort Applications** - For scholarship program applicants
  - **Intern Applications** - For internship program applicants
- **Application Progress Dashboard** - Visual tracking of form completion status
- **Document Upload** - Support for uploading required documents (transcripts, certificates, recommendation letters, IDs)
- **Application Submission** - Secure submission with digital signature

### For Administrators
- **Admin Dashboard** - View and manage all applications
- **Portal Control** - Open/close application portal with configurable deadlines
- **User Management** - Activate users, manage accounts
- **Bulk Email System** - Send customized emails to applicants
- **Application Settings** - Configure application periods and deadlines

## 🛠️ Tech Stack

- **Backend**: Python 3.10+, Django 5.1.3
- **Database**: MySQL
- **Frontend**: HTML5, CSS3, Bootstrap 5, JavaScript
- **Authentication**: Django's built-in auth with custom user model
- **Email**: SMTP email integration
- **Static Files**: WhiteNoise for production static file serving
- **Form Handling**: Django Crispy Forms with Bootstrap 5

## 📁 Project Structure

```
TanSAF-Application-Portal/
├── TanSAFApply/              # Main Django project settings
│   ├── settings.py           # Django configuration
│   ├── urls.py               # Main URL routing
│   └── wsgi.py               # WSGI configuration
├── yuzzaz/                   # Core app (users, auth, homepage)
│   ├── models.py             # CustomUser and ApplicationSettings models
│   ├── views.py              # Authentication and portal views
│   ├── forms.py              # User registration and email forms
│   ├── templates/            # HTML templates
│   └── tokens.py             # Account activation tokens
├── application_cohort/       # Cohort application app
│   ├── models.py             # ApplicationCohort, Sibling, Activity, etc.
│   ├── views.py              # Application form views
│   ├── forms.py              # Application forms
│   └── templates/            # Cohort-specific templates
├── application_intern/       # Internship application app
│   ├── models.py             # ApplicationIntern and related models
│   ├── views.py              # Intern application views
│   └── templates/            # Intern-specific templates
├── static/                   # Static assets (CSS, JS, images)
├── staticfiles/              # Collected static files (production)
├── manage.py                 # Django CLI utility
└── passenger_wsgi.py         # Production WSGI entry point
```

## 🚀 Installation

### Prerequisites

- Python 3.10+
- MySQL Server
- pip (Python package manager)
- Virtual environment (recommended)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/gcl140/TanSAF-Application-Portal.git
   cd TanSAF-Application-Portal
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Python dependencies**
   ```bash
   pip install django mysqlclient python-decouple django-phonenumber-field phonenumbers django-widget-tweaks django-crispy-forms crispy-bootstrap5 whitenoise
   ```

   > **Tip**: For reproducible builds, consider creating a `requirements.txt` file with pinned versions.

4. **Configure environment variables**
   
   Create a `.env` file in the project root:
   ```env
   EMAIL_HOST_USER=your-email@example.com
   EMAIL_HOST_PASSWORD=your-email-password
   DB_NAME=your_database_name
   DB_USER=your_database_user
   DB_PASSWORD=your_database_password
   DB_HOST=localhost
   DB_PORT=3306
   ```

5. **Configure the database**
   
   Update `TanSAFApply/settings.py` to use environment variables for database credentials:
   ```python
   from decouple import config

   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': config('DB_NAME'),
           'USER': config('DB_USER'),
           'PASSWORD': config('DB_PASSWORD'),
           'HOST': config('DB_HOST', default='localhost'),
           'PORT': config('DB_PORT', default='3306'),
       }
   }
   ```

6. **Run database migrations**
   ```bash
   python manage.py migrate
   ```

7. **Collect static files**
   ```bash
   python manage.py collectstatic
   ```

8. **Create a superuser**
   ```bash
   python manage.py createsuperuser
   ```

9. **Run the development server**
   ```bash
   python manage.py runserver
   ```

   Visit `http://127.0.0.1:8000` in your browser.

## ⚙️ Configuration

### Development Settings

For local development, update `settings.py`:
```python
DEBUG = True
ALLOWED_HOSTS = ['127.0.0.1', 'localhost']
```

### Production Settings

For production deployment:
```python
DEBUG = False
ALLOWED_HOSTS = ['your-domain.com', 'www.your-domain.com']
```

### Email Configuration

The application uses SMTP for sending activation emails. Configure your email settings in `settings.py`:
```python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'your-smtp-host'
EMAIL_PORT = 465
EMAIL_USE_SSL = True
```

## 📝 Usage

### For Applicants

1. Visit the homepage and select your application type (Cohort or Intern)
2. Register with your email address
3. Activate your account via the email link
4. Complete all sections of the application form
5. Upload required documents
6. Review and submit your application

### For Administrators

1. Access the admin panel at `/admin/`
2. Manage application settings via the portal settings page
3. View and review submitted applications
4. Send bulk emails to applicants
5. Control portal open/close status

## 📋 Application Sections

The application form includes the following sections:
- **Introduction** - Terms and conditions agreement
- **General Information** - Personal details
- **Contact Information** - Address and phone numbers
- **School Information** - Education history (O-Level & A-Level)
- **Family Information** - Parent/guardian details
- **Siblings & Dependents** - Family members
- **Financial Information** - Financial background
- **Activities & Distinctions** - Extracurricular activities and awards
- **Writing Section** - Essays and personal statements
- **Files & Signature** - Document uploads and digital signature

## 🔒 Security Notes

- Always use environment variables for sensitive data
- Change the `SECRET_KEY` in production
- Use HTTPS in production
- Regularly update dependencies

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Gift Christian** - [gcl140](https://github.com/gcl140)

---

*Built with ❤️ for Tanzania Scholars Alumni Foundation*