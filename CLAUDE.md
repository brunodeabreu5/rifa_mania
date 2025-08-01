# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Laravel 12 application called "Rifa Mania" - an online raffle management system specifically designed for Paraguay. The project features a modern multilingual platform supporting Portuguese (Brazil), English, and Spanish (Paraguay), built with modern Laravel features. The system uses SQLite as the default database and includes a modern frontend stack with Vite and Tailwind CSS 4.0.

### Key Features

-   **Online Raffle System**: Complete raffle creation, management, and drawing functionality
-   **Paraguay Market Focus**: Tailored for Paraguayan regulations and payment methods
-   **Multilingual Support**: Portuguese (BR), English (US), and Spanish (PY)
-   **Modern UI**: Responsive design with Tailwind CSS 4.0
-   **Real-time Updates**: Live raffle status and participant updates

## Development Commands

### Server & Development

```bash
# Start development server with hot reload (includes server, queue, logs, and vite)
composer run dev

# Alternative: Start Laravel development server only
php artisan serve

# Start Vite development server for frontend assets
npm run dev

# Build frontend assets for production
npm run build
```

### Database & Migrations

```bash
# Run database migrations
php artisan migrate

# Run migrations with graceful handling
php artisan migrate --graceful

# Fresh migration (drops all tables and re-runs migrations)
php artisan migrate:fresh

# Generate new migration
php artisan make:migration create_table_name

# Rollback last migration
php artisan migrate:rollback
```

### Internationalization (i18n)

```bash
# Publish language files
php artisan lang:publish

# Generate translation files for new language
php artisan make:lang es_PY

# Extract translatable strings from views
php artisan lang:extract

# Validate translation completeness
php artisan lang:validate

# Clear translation cache
php artisan cache:clear
```

### Testing

```bash
# Run all tests
composer run test
# or
php artisan test

# Run specific test file
php artisan test tests/Feature/ExampleTest.php

# Run tests with coverage
php artisan test --coverage

# Run multilingual tests
php artisan test --filter=LanguageTest
```

### Code Quality

```bash
# Format code with Laravel Pint
./vendor/bin/pint

# Check code style without fixing
./vendor/bin/pint --test
```

### Artisan Commands

```bash
# Generate application key
php artisan key:generate

# Clear application cache
php artisan cache:clear

# Clear configuration cache
php artisan config:clear

# Clear route cache
php artisan route:clear

# Clear view cache
php artisan view:clear

# Generate new controller
php artisan make:controller ControllerName

# Generate new model with migration
php artisan make:model ModelName -m

# Generate new seeder
php artisan make:seeder SeederName

# Run database seeders
php artisan db:seed

# Generate raffle-specific components
php artisan make:controller RaffleController --resource
php artisan make:model Raffle -m
php artisan make:model Participant -m
php artisan make:model RaffleTicket -m
```

## Architecture & Configuration

### Database Configuration

-   **Default connection**: SQLite (`database/database.sqlite`)
-   **Alternative**: MySQL configuration available for production
-   Configured to use database for sessions, cache, and queue storage
-   **Raffle-specific tables**: raffles, participants, raffle_tickets, payments

### Multilingual Configuration

-   **Supported Languages**:
    -   Portuguese (Brazil) - `pt_BR`
    -   English (US) - `en`
    -   Spanish (Paraguay) - `es_PY`
-   **Default locale**: Spanish (Paraguay) for local market
-   **Fallback locale**: English
-   **Language files**: `lang/pt_BR/`, `lang/en/`, `lang/es_PY/`
-   **Route localization**: Enabled for SEO optimization

### Frontend Stack

-   **Build tool**: Vite with Laravel plugin
-   **CSS framework**: Tailwind CSS 4.0 with RTL support
-   **Entry points**: `resources/css/app.css`, `resources/js/app.js`
-   **Hot reload**: Enabled via Laravel Vite plugin
-   **Language switching**: Dynamic locale switching without page reload

### Environment Setup

-   Uses `.env` file for configuration (copy from `.env.example`)
-   Default locale: Spanish Paraguay (`es_PY`)
-   Debug mode enabled in local environment
-   Queue connection: database
-   Cache store: database
-   Session driver: database
-   **Paraguay-specific configs**:
    -   Timezone: `America/Asuncion`
    -   Currency: PYG (Paraguayan Guarani)
    -   Payment gateways for Paraguay market

### Project Structure

-   **Models**: `app/Models/` - Eloquent models
    -   `Raffle.php` - Main raffle model
    -   `Participant.php` - Raffle participants
    -   `RaffleTicket.php` - Individual tickets
    -   `Payment.php` - Payment processing
-   **Controllers**: `app/Http/Controllers/` - HTTP request handlers
    -   `RaffleController.php` - Raffle management
    -   `ParticipantController.php` - Participant registration
    -   `PaymentController.php` - Payment processing
    -   `LocaleController.php` - Language switching
-   **Views**: `resources/views/` - Blade templates
    -   `raffles/` - Raffle-related views
    -   `components/` - Reusable components
-   **Routes**: `routes/web.php` - Web routes definition
-   **Migrations**: `database/migrations/` - Database schema changes
-   **Seeders**: `database/seeders/` - Database seeders
-   **Language Files**: `lang/` - Translation files
    -   `pt_BR/` - Portuguese (Brazil) translations
    -   `en/` - English translations
    -   `es_PY/` - Spanish (Paraguay) translations
-   **Tests**: `tests/Feature/` and `tests/Unit/` - PHPUnit tests

### Raffle System Features

-   **Raffle Management**: Create, edit, publish raffles
-   **Ticket Sales**: Online ticket purchasing system
-   **Payment Integration**: Local Paraguay payment methods
-   **Draw System**: Automated and manual drawing options
-   **Participant Management**: Registration and ticket tracking
-   **Reporting**: Sales reports and analytics
-   **Legal Compliance**: Paraguay raffle regulations compliance

### Development Tools

-   **Laravel Pint**: Code formatting (PSR-12 standard)
-   **Laravel Pail**: Log monitoring
-   **Laravel Tinker**: REPL for Laravel
-   **Concurrently**: Runs multiple dev processes simultaneously

## Dependencies

### Core Dependencies

-   Laravel Framework ^12.0
-   PHP ^8.2
-   Laravel Localization package
-   Currency formatting for PYG

### Development Tools

-   Laravel Pint (code formatting)
-   Laravel Sail (Docker environment)
-   Laravel Pail (log monitoring)
-   PHPUnit (testing)
-   Faker (test data generation)

### Paraguay-specific Integrations

-   Payment gateway integrations for Paraguay
-   SMS/WhatsApp notifications (popular in Paraguay)
-   Geographic data for Paraguay regions
-   Local bank integration APIs

## Deployment Notes

-   Configure proper timezone for Paraguay (`America/Asuncion`)
-   Set up SSL certificates for secure payments
-   Configure email services for Spanish and Portuguese
-   Set up monitoring for raffle draws and payments
-   Ensure compliance with Paraguay gaming/raffle regulations
