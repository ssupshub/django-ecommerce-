# Django eCommerce

Welcome to the Django eCommerce project! This repository contains a robust eCommerce platform built using Django, designed to provide a seamless online shopping experience similar to popular clothing websites like Myntra, Flipkart, and Amazon.

## Features

- **Product Listings:** Showcase a variety of clothing items with detailed descriptions and images.
- **User Accounts:** Users can create accounts, log in, and manage their profiles.
- **Shopping Cart:** Users can add items to their cart and proceed to checkout.
- **Order Management:** Admins can manage orders and update their statuses.
- **Payment Integration:** Supports integration with payment gateways for secure transactions.
- **Responsive Design:** Optimized for a smooth experience on both desktop and mobile devices.

## Technologies Used

- **Django:** The web framework used to build the backend of the application.
- **Python:** The programming language for developing the application.
- **Gunicorn:** The WSGI HTTP server used to serve the Django application.
- **Nginx:** The web server used to handle static files and proxy requests to Gunicorn.
- **Certbot:** Used for obtaining and renewing SSL certificates to ensure secure communication.

## Getting Started

### Prerequisites

Ensure you have the following installed:

- Python 3.x
- Django
- Gunicorn
- Nginx
- Certbot

### Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/your-username/django-ecommerce.git
   cd django-ecommerce
   ```

2. **Create and Activate a Virtual Environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate
   ```

3. **Install Dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Environment Variables:**

   Create a `.env` file in the root directory and add your environment-specific settings, including database credentials and secret keys.

5. **Run Migrations:**

   ```bash
   python manage.py migrate
   ```

6. **Collect Static Files:**

   ```bash
   python manage.py collectstatic
   ```

7. **Start the Development Server:**

   ```bash
   python manage.py runserver
   ```

   For production, you'll configure Gunicorn and Nginx as described in the [Deployment](#deployment) section.

## Deployment

1. **Set Up Gunicorn:**

   Install Gunicorn if it's not already installed:

   ```bash
   pip install gunicorn
   ```

   Run Gunicorn:

   ```bash
   gunicorn --workers 3 myproject.wsgi:application
   ```

2. **Configure Nginx:**

   Create an Nginx configuration file (e.g., `/etc/nginx/sites-available/django-ecommerce`) with the following content:

   ```nginx
   server {
       listen 80;
       server_name your_domain.com;

       location = /favicon.ico { access_log off; log_not_found off; }
       location /static/ {
           root /path/to/your/project;
       }

       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```

   Link the configuration file and restart Nginx:

   ```bash
   sudo ln -s /etc/nginx/sites-available/django-ecommerce /etc/nginx/sites-enabled
   sudo systemctl restart nginx
   ```

3. **Set Up SSL with Certbot:**

   Install Certbot and obtain an SSL certificate:

   ```bash
   sudo apt-get install certbot python3-certbot-nginx
   sudo certbot --nginx -d your_domain.com
   ```


## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your proposed changes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any inquiries, please reach out to my instagram ssupshub.

---

Feel free to customize the paths, domain names, and any other project-specific details according to your actual setup and preferences.
