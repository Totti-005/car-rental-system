# Pro Car — Online Car Rental System

Modern, responsive car rental platform built with:

- **Frontend:** HTML5, CSS3, JavaScript, Bootstrap 5
- **Backend:** PHP
- **Database:** MySQL via WAMP local server

## Features

### User Roles

- **Customers:** Register, browse cars, book vehicles, view bookings, make payments
- **Company:** Manage inventory, set prices, monitor bookings
- **Admin:** Manage users, cars, bookings, and generate reports

### Core Features

1. **User Registration & Authentication** - Secure login/register with password hashing
2. **Car Search & Browsing** - Filter by category, price, year
3. **Booking Management** - Create, view, and cancel bookings
4. **Payment Processing** - Track payment status
5. **Admin Dashboard** - Manage cars, bookings, and users
6. **Responsive Design** - Modern dark theme with amber accents (matching Hire With Us)

## Installation

### Prerequisites

- PHP 8.4+
- WAMP or another MySQL-enabled local server stack
- Web browser

### Setup Steps

1. Start WAMP and make sure MySQL is running.
2. Run the app from the project root with a PHP development server:

```bash
cd "path/to/pro car"
php -S localhost:80
```

3. Open the app in your browser:

```text
http://localhost/index.html
```

## Project Structure

```
pro car/
├── index.html                  # Home page
├── cars.html                   # Car browsing & booking
├── dashboard.html              # User/Admin dashboard
├── review.html                 # Customer review flow
├── auth/
│   ├── login.html              # Login page
│   └── register.html           # Registration page
├── backend/
│   ├── db.php                  # Database connection and schema bootstrap
│   ├── auth.php                # Authentication API
│   ├── cars_api.php            # Cars CRUD API
│   ├── bookings.php            # Bookings API
│   ├── payments.php            # Payments API
│   ├── reviews.php             # Review endpoint
│   └── reports.php             # Admin summary reports
├── css/
│   └── style.css               # Main stylesheet (dark theme)
├── js/
│   ├── api.js                  # API base path helper
│   ├── app.js                  # Home page logic
│   ├── auth.js                 # Auth page logic
│   ├── cars.js                 # Cars page logic
│   ├── dashboard.js            # Dashboard logic
│   └── review.js               # Review summary helpers
└── README.md
```

## Database Schema

### Key Tables

- `users` - Customers, drivers, admins, company staff
- `cars` - Vehicle inventory
- `bookings` - Rental bookings
- `payments` - Payment records
- `ratings` - User reviews
- `roles` - User role definitions
- `companies` - Rental companies

## API Endpoints

### Authentication

- `POST backend/auth.php?action=register` - Register new user
- `POST backend/auth.php?action=login` - User login
- `POST backend/auth.php?action=logout` - User logout

### Cars

- `GET backend/cars_api.php` - List cars with filters (category, price, year)
- `GET backend/cars_api.php?admin=1` - List all cars (admin)
- `POST backend/cars_api.php` - Add car (admin)
- `PUT backend/cars_api.php` - Update car (admin)
- `DELETE backend/cars_api.php` - Delete car (admin)

### Bookings

- `GET backend/bookings.php?user_id=ID` - Get user bookings
- `GET backend/bookings.php?admin=1` - Get all bookings (admin)
- `POST backend/bookings.php` - Create booking
- `PUT backend/bookings.php` - Update booking status (admin)
- `DELETE backend/bookings.php` - Cancel booking

### Payments

- `GET backend/payments.php?booking_id=ID` - Get payment info
- `POST backend/payments.php` - Create payment

## Testing

### Test Credentials

**Admin Account:**

- Email: admin@procar.local
- Password: Admin@123

**Sample Car:**

- Make: Toyota
- Model: Corolla
- Year: 2020
- Category: Sedan
- Price: $35/day

Insert via SQL:

```sql
INSERT INTO users (name, email, phone, password_hash, role_id, is_active)
VALUES ('Admin', 'admin@procar.local', '0123456789', '$2y$10$...', 4, 1);
```

## Features Demo

1. **Home Page** - View featured cars and statistics
2. **Register** - Create customer or company account
3. **Browse Cars** - Search and filter vehicles
4. **Book Car** - Select dates and complete booking
5. **Dashboard** - View bookings and manage account
6. **Admin Panel** - Manage cars, bookings, users

## Security Notes

### Important

⚠️ **This is a development system. Before production:**

1. Enable HTTPS/SSL
2. Implement rate limiting
3. Add CSRF tokens to all forms
4. Validate/sanitize all inputs
5. Implement proper session management
6. Use environment variables for credentials
7. Add request logging and monitoring
8. Implement backup and recovery procedures

### Example Improvements

```php
// Add to backend/db.php for security
session_start();
$_SESSION['csrf_token'] = bin2hex(random_bytes(32));

// Validate tokens
if (!hash_equals($_SESSION['csrf_token'], $_POST['csrf_token'])) {
  die('Invalid request');
}
```

## Deployment

### Using WAMP

1. Copy the project into `C:\wamp64\www\procar`
2. Start Apache and MySQL from the WAMP control panel
3. Open `http://localhost/procar/index.html`

### Using the local PHP server

```bash
cd "path/to/pro car"
php -S 127.0.0.1:8080 -t .
```

Then open:

```text
http://127.0.0.1:8080/index.html
```

If port 8080 is in use, choose another free port and update the URL accordingly.

### Cloud Deployment

- **Heroku:** Use Procfile + buildpacks
- **AWS:** EC2 + RDS MySQL
- **DigitalOcean:** App Platform or Droplet

## Troubleshooting

### Database Connection Error

- Check MySQL is running
- Verify credentials in `backend/db.php`
- Ensure database exists: `pro_car`

### 404 on PHP Endpoints

- Verify WAMP Apache is running
- Check file paths are correct
- Ensure all backend files exist

### Login/Register Not Working

- Clear browser localStorage: `localStorage.clear()`
- Check browser console for errors (F12)
- Verify database connection

## Development Notes

### Local Testing Workflow

```bash
# 1. Start WAMP and ensure Apache + MySQL are running
# 2. Open browser
# http://localhost/procar/index.html
# or http://procar.local if configured

# 3. Test endpoints with curl
curl -X GET http://localhost/procar/backend/cars_api.php

# 4. View database
mysql -u root -p pro_car
SELECT * FROM cars;
```

### File Modifications

All frontend changes reload instantly. For PHP changes:

1. Save file
2. Refresh browser page
3. Check error logs: `php -d error_reporting=E_ALL`

## Contributing

To add features:

1. Create new HTML page or component
2. Add corresponding JavaScript logic
3. Create/extend PHP API endpoint
4. Add database tables if needed
5. Update README with changes

## License

Educational project - Feel free to use and modify.

## Support

For issues or questions:

1. Check error messages in browser console (F12)
2. Review database schema in `sql/schema_full.sql`
3. Check backend logs with PHP verbose mode
4. Review API endpoints documentation above

## Troubleshooting

### Issue: "Failed to execute 'json' on 'Response': Unexpected end of JSON input"

**Causes & Solutions:**

1. **Database Not Running**
   - Start MySQL/XAMPP first
   - Error handling now shows: "Database connection failed"
   - All API calls validate response before parsing

2. **Invalid API Response**
   - Check browser console (F12 → Console tab) for full error
   - Look for HTTP status codes (404, 500, etc.)
   - Backend now returns valid JSON on all errors

3. **CORS Issues**
   - Headers already set in `backend/db.php` and all API files
   - If still seeing errors, check server logs

4. **Empty Response**
   - Frontend validates data type before using
   - Error messages now display on page instead of silent failures

**Quick Fix Checklist:**

- [ ] XAMPP MySQL is running (Control Panel)
- [ ] Database imported: `mysql -u root < sql/schema_full.sql`
- [ ] db.php credentials match your MySQL setup
- [ ] Browser console shows no errors (F12)
- [ ] Check network tab (F12 → Network) for failed requests
- [ ] Clear browser cache: Ctrl+Shift+Delete

### Issue: Blank Pages or Missing Cars

- Open browser console (F12)
- Look for error messages
- Check Network tab to see API response status
- Ensure database has data: `mysql -u root -p pro_car`

### Issue: Login/Register Not Working

- Clear browser localStorage: `localStorage.clear()` in console
- Check if email already exists in database
- Verify form has all required fields
- Check backend error message in Network response

### Feature: Error Handling Improvements

All JavaScript files now:

- Check HTTP status before parsing JSON
- Validate response data type
- Display user-friendly error messages
- Log detailed errors to console for debugging

### Database Setup Alternatives

**Option 1: phpMyAdmin (GUI)**

1. Open http://localhost/phpmyadmin
2. Create database: pro_car
3. Import sql/schema_full.sql

**Option 2: MySQL Command Line**

```bash
mysql -u root
CREATE DATABASE pro_car;
USE pro_car;
SOURCE sql/schema_full.sql;
```

**Option 3: MySQL GUI Tools**

- MySQL Workbench
- DataGrip
- DBeaver
