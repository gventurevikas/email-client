# Email Client System

A comprehensive email client system built with Node.js, Angular, MySQL, and Kafka for handling email operations with a custom SMTP server.

## System Architecture

### Components
- **Frontend**: Angular 17+ application
- **Backend**: Node.js with Express.js based on typescript
- **Database**: MySQL 8.0+
- **Message Queue**: Apache Kafka (email sink to db/send email via smtp client)
- **Email Processing**: Custom SMTP server integration
- **Authentication**: JWT-based authentication
- **File Storage**: Local file system for attachments

### Architecture Diagram
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Angular UI    │    │   Node.js API   │    │   MySQL DB      │
│   (Frontend)    │◄──►│   (Backend)     │◄──►│   (Database)    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       ▼                       │
         │              ┌─────────────────┐             │
         │              │   Kafka Queue   │             │
         │              │   (Message      │             │
         │              │    Broker)      │             │
         │              └─────────────────┘             │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   File Storage  │    │  SMTP Server    │    │   Email Sink    │
│  (Attachments)  │    │  (Custom)       │    │   (Kafka)       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## Features

### Core Email Features
- ✅ Send emails with attachments
- ✅ Receive and display emails
- ✅ Email threading and conversations
- ✅ Rich text editor for composing emails
- ✅ Email templates
- ✅ Draft management
- ✅ Email search and filtering
- ✅ Email labels and folders
- ✅ Email forwarding and replying

### Advanced Features
- ✅ Real-time email notifications
- ✅ Email scheduling
- ✅ Email analytics and tracking
- ✅ Bulk email operations
- ✅ Email encryption
- ✅ Spam filtering
- ✅ Auto-reply functionality
- ✅ Email archiving

### User Management
- ✅ User registration and authentication
- ✅ Role-based access control
- ✅ User profiles and preferences
- ✅ Multi-tenant support

## Technology Stack

### Frontend
- **Framework**: Angular 17+
- **UI Library**: Angular Material
- **State Management**: NgRx
- **HTTP Client**: Angular HttpClient
- **Real-time**: WebSocket (Socket.io)
- **Rich Text Editor**: Quill.js
- **File Upload**: ngx-file-drop

### Backend
- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Authentication**: JWT, bcrypt
- **Email Processing**: Nodemailer, SMTP
- **File Handling**: Multer, Sharp
- **Validation**: Joi
- **Testing**: Jest, Supertest

### Database
- **Database**: MySQL 8.0+
- **ORM**: Sequelize
- **Migrations**: Sequelize CLI
- **Seeding**: Custom seeders

### Message Queue
- **Broker**: Apache Kafka
- **Client**: kafkajs
- **Topics**: email-send, email-receive, notifications
- **Consumer Groups**: email-processors

### DevOps & Tools
- **Containerization**: Docker, Docker Compose
- **Environment**: Environment variables
- **Logging**: Winston
- **Monitoring**: Prometheus, Grafana
- **CI/CD**: GitHub Actions

## Project Structure

```
email-client/
├── frontend/                 # Angular application
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/   # Reusable components
│   │   │   ├── services/     # API services
│   │   │   ├── store/        # NgRx store
│   │   │   ├── models/       # TypeScript interfaces
│   │   │   └── guards/       # Route guards
│   │   ├── assets/           # Static assets
│   │   └── environments/     # Environment configs
│   ├── package.json
│   └── angular.json
├── backend/                  # Node.js API
│   ├── src/
│   │   ├── controllers/      # Route controllers
│   │   ├── models/          # Database models
│   │   ├── services/        # Business logic
│   │   ├── middleware/      # Custom middleware
│   │   ├── routes/          # API routes
│   │   ├── utils/           # Utility functions
│   │   └── config/          # Configuration files
│   ├── migrations/          # Database migrations
│   ├── seeders/            # Database seeders
│   └── package.json
├── kafka/                   # Kafka configurations
│   ├── docker-compose.yml
│   ├── topics/             # Topic definitions
│   └── scripts/            # Kafka scripts
├── database/               # Database scripts
│   ├── init.sql           # Database initialization
│   └── migrations/        # SQL migrations
├── docker-compose.yml      # Development environment
├── .env.example           # Environment variables template
└── README.md              # This file
```

## Quick Start

### Prerequisites
- Node.js 18+ (typescript based)
- MySQL 8.0+
- Docker & Docker Compose
- Angular CLI
- Git

### Development Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd email-client
```

2. **Set up environment variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

3. **Start development environment**
```bash
# Start all services (MySQL, Kafka, Backend, Frontend)
docker-compose up -d

# Or start services individually
docker-compose up mysql kafka -d
npm run dev:backend
npm run dev:frontend
```

4. **Initialize database**
```bash
npm run db:migrate
npm run db:seed
```

5. **Access the application**
- Frontend: http://localhost:4200
- Backend API: http://localhost:3000
- Kafka UI: http://localhost:8080
- MySQL: localhost:3306

## API Documentation

### Authentication Endpoints
```
POST /api/auth/register     # User registration
POST /api/auth/login        # User login
POST /api/auth/logout       # User logout
POST /api/auth/refresh      # Refresh token
```

### Email Endpoints
```
GET    /api/emails          # Get emails (with pagination)
POST   /api/emails          # Send email
GET    /api/emails/:id      # Get specific email
PUT    /api/emails/:id      # Update email (draft)
DELETE /api/emails/:id      # Delete email
POST   /api/emails/:id/reply    # Reply to email
POST   /api/emails/:id/forward  # Forward email
```

### User Endpoints
```
GET    /api/users/profile   # Get user profile
PUT    /api/users/profile   # Update user profile
GET    /api/users/settings  # Get user settings
PUT    /api/users/settings  # Update user settings
```

## Database Schema

### Core Tables
- `users` - User accounts and profiles
- `emails` - Email messages
- `email_attachments` - Email attachments
- `email_recipients` - Email recipients (TO, CC, BCC)
- `email_labels` - Email labels and folders
- `email_threads` - Email conversation threads

### Supporting Tables
- `user_settings` - User preferences
- `email_templates` - Email templates
- `email_schedules` - Scheduled emails
- `email_analytics` - Email tracking data

## Kafka Topics

### Email Processing
- `email-send` - Outgoing emails
- `email-receive` - Incoming emails
- `email-notifications` - Email notifications

### System Events
- `user-events` - User activity events
- `system-events` - System maintenance events

## Deployment

### Production Setup
1. **Environment Configuration**
   - Set production environment variables
   - Configure SSL certificates
   - Set up monitoring and logging

2. **Database Setup**
   - Create production MySQL instance
   - Run migrations
   - Set up database backups

3. **Kafka Setup**
   - Configure Kafka cluster
   - Set up topic replication
   - Configure consumer groups

4. **Application Deployment**
   - Build Angular application
   - Deploy Node.js application
   - Set up reverse proxy (Nginx)
   - Configure load balancing

### Docker Deployment
```bash
# Build and deploy with Docker
docker-compose -f docker-compose.prod.yml up -d
```

## Monitoring & Logging

### Application Monitoring
- **Health Checks**: `/api/health`
- **Metrics**: Prometheus endpoints
- **Logging**: Winston with structured logging
- **Error Tracking**: Custom error handling

### Database Monitoring
- **Query Performance**: Slow query logging
- **Connection Pooling**: Monitor connection usage
- **Backup Monitoring**: Automated backup verification

### Kafka Monitoring
- **Topic Metrics**: Message rates, lag
- **Consumer Groups**: Consumer lag monitoring
- **Broker Health**: Cluster health checks

## Security Considerations

### Authentication & Authorization
- JWT tokens with refresh mechanism
- Role-based access control (RBAC)
- API rate limiting
- CORS configuration

### Data Security
- Email encryption at rest
- Secure file upload handling
- SQL injection prevention
- XSS protection

### Infrastructure Security
- HTTPS/TLS encryption
- Database connection encryption
- Kafka SASL authentication
- Docker security best practices

## Testing Strategy

### Unit Testing
- **Frontend**: Jasmine/Karma
- **Backend**: Jest
- **Database**: Integration tests

### Integration Testing
- **API Testing**: Supertest
- **E2E Testing**: Playwright
- **Kafka Testing**: Test containers

### Performance Testing
- **Load Testing**: Artillery
- **Database Testing**: Custom benchmarks
- **Email Processing**: Throughput testing

## Contributing

### Development Workflow
1. Create feature branch
2. Implement changes
3. Write tests
4. Update documentation
5. Submit pull request

### Code Standards
- **Frontend**: ESLint, Prettier
- **Backend**: ESLint, Prettier
- **Database**: SQL formatting standards
- **Git**: Conventional commits

## Troubleshooting

### Common Issues
1. **Database Connection**: Check MySQL service and credentials
2. **Kafka Connection**: Verify Kafka broker status
3. **Email Sending**: Check SMTP configuration
4. **File Upload**: Verify storage permissions

### Debug Commands
```bash
# Check service status
docker-compose ps

# View logs
docker-compose logs [service-name]

# Database connection test
npm run db:test

# Kafka topic verification
npm run kafka:topics:list
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions:
- Create an issue in the repository
- Check the troubleshooting section
- Review the API documentation
- Contact the development team 