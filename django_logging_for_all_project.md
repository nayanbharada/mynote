
# Django project logging 
How we can setup a django logging for project here is the steps

## Steps
- Need to configure in settings.py

```bash
LOGGING_DIR = os.path.join(BASE_DIR, 'logs')  # The directory where log files will be stored
if not os.path.exists(LOGGING_DIR):
    os.makedirs(LOGGING_DIR)

```
- this code through our root structure in logs dir create

- after this we need to create log level folder structure
```bash
def get_log_filename(folder_name, file_name):
    """log file name and dir create"""
    now = datetime.now()
    log_level_folder = os.path.join(LOGGING_DIR, folder_name.lower())
    if not os.path.exists(log_level_folder):
        os.makedirs(log_level_folder)
    return os.path.join(LOGGING_DIR, folder_name.lower(), f"{now.strftime('%Y-%m')}_{file_name}")
```

- logging configuration need to add in settings.py

```bash
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'formatters': {
        'verbose': {
            'format': '{levelname} {asctime} {module} {message}',
            'style': '{',
        },
    },
    'handlers': {
        'debug_file': {
            'level': 'DEBUG',
            'class': 'logging.handlers.RotatingFileHandler',
            # 'filename': os.path.join(LOGGING_DIR, 'debug.log'),
            'filename': get_log_filename("debug", "debug.log"),
            'formatter': 'verbose',
            'maxBytes': 1024 * 1024 * 10,  # 10 MB (adjust as needed)
            'backupCount': 5,  # Number of backup log files to keep
        },
        'info_file': {
            'level': 'INFO',
            'class': 'logging.handlers.RotatingFileHandler',
            # 'filename': os.path.join(LOGGING_DIR, 'info.log'),
            'filename': get_log_filename("info", "info.log"),
            'formatter': 'verbose',
            'maxBytes': 1024 * 1024 * 10,  # 10 MB (adjust as needed)
            'backupCount': 5,  # Number of backup log files to keep
        },
        'warning_file': {
            'level': 'WARNING',
            'class': 'logging.handlers.RotatingFileHandler',
            # 'filename': os.path.join(LOGGING_DIR, 'warning.log'),
            'filename': get_log_filename("warning", "warning.log"),
            'formatter': 'verbose',
            'maxBytes': 1024 * 1024 * 10,  # 10 MB (adjust as needed)
            'backupCount': 5,  # Number of backup log files to keep
        },
        'error_file': {
            'level': 'ERROR',
            'class': 'logging.handlers.RotatingFileHandler',
            # 'filename': os.path.join(LOGGING_DIR, 'error.log'),
            'filename': get_log_filename("error", "error.log"),
            'formatter': 'verbose',
            'maxBytes': 1024 * 1024 * 10,  # 10 MB (adjust as needed)
            'backupCount': 5,  # Number of backup log files to keep
        },
        # # for console error
        # 'console': {
        #     'level': 'DEBUG',
        #     'class': 'logging.StreamHandler',
        # },
    },
    'root': {
        # 'handlers': ['debug_file', 'info_file', 'warning_file', 'error_file','console'],
        'handlers': ['debug_file', 'info_file', 'warning_file', 'error_file'],
        'level': 'DEBUG',
        'propagate': True
    },
}
```

- after this we need to execute for views.py

```bash
import logging
logger = logging.getLogger(__name__)


def get(self, request, *args, **kwargs):
    logger.debug("nayan debug error message test")
    logger.info("nayan info error message test")
    logger.error("nayan error message test")
    logger.warning("nayan warning mesaage test")
    return render(request, self.template_name)
```


