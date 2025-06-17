# HomeWiz Backend - Comprehensive Documentation

## 📋 Project Overview

**HomeWiz Backend** is a sophisticated FastAPI-based property management system designed for rental property operations. It combines traditional property management features with AI-powered search capabilities using Google's Gemini API.

### Key Features
- 🏢 **Property Management**: Buildings, rooms, tenants, operators
- 🎯 **Lead Management**: Prospective tenant tracking and conversion
- 🔧 **Maintenance Operations**: Request tracking and assignment
- 🤖 **AI Integration**: Natural language query processing for room searches
- 💬 **Communication**: Messages, notifications, announcements
- 📄 **Document Management**: Lease generation, applications

## 🛠 Technology Stack

| Component | Technology | Version |
|-----------|------------|---------|
| **Framework** | FastAPI | 0.115.11 |
| **Database** | PostgreSQL (Supabase) | - |
| **ORM** | SQLAlchemy | 2.0.23 |
| **AI Integration** | Google Gemini API | 1.3.0 |
| **Validation** | Pydantic | 2.10.6 |
| **Testing** | pytest | 8.3.5 |
| **Server** | Uvicorn | 0.34.0 |
| **Environment** | Python | 3.11+ |

## 📁 Project Structure

```
homewiz-backend/
├── app/
│   ├── __init__.py
│   ├── main.py                 # FastAPI application entry point
│   ├── config.py              # Configuration management
│   ├── ai_dispatcher.py       # AI function routing
│   ├── ai_functions.py        # AI-powered functions
│   ├── db/
│   │   ├── __init__.py
│   │   ├── connection.py      # Database connection setup
│   │   ├── models.py          # SQLAlchemy ORM models
│   │   └── scripts/
│   │       ├── seed_db.py     # Database seeding
│   │       └── check_tables.py
│   ├── endpoints/             # API route handlers
│   │   ├── __init__.py
│   │   ├── buildings.py
│   │   ├── rooms.py
│   │   ├── tenants.py
│   │   ├── leads.py
│   │   ├── operators.py
│   │   ├── query.py           # AI-powered search endpoint
│   │   ├── maintenance.py
│   │   ├── notifications.py
│   │   ├── scheduling.py
│   │   ├── checklists.py
│   │   ├── documents.py
│   │   ├── messages.py
│   │   ├── announcements.py
│   │   └── analytics.py
│   ├── middleware/            # Request/response middleware
│   │   ├── __init__.py
│   │   ├── auth.py           # Authentication (empty)
│   │   └── logging.py        # Logging (empty)
│   ├── models/               # Pydantic schemas
│   │   ├── __init__.py
│   │   ├── building.py
│   │   ├── room.py
│   │   ├── tenant.py
│   │   ├── lead.py
│   │   ├── operator.py
│   │   ├── maintenance_request.py
│   │   ├── notification.py
│   │   ├── scheduled_event.py
│   │   ├── checklist.py
│   │   ├── document.py
│   │   ├── message.py
│   │   ├── announcement.py
│   │   └── query.py
│   └── services/             # Business logic layer
│       ├── __init__.py
│       ├── building_service.py
│       ├── room_service.py
│       ├── tenant_service.py
│       ├── lead_service.py
│       ├── operator_service.py
│       ├── maintenance_service.py
│       ├── notification_service.py
│       ├── scheduling_service.py
│       ├── checklist_service.py
│       ├── document_service.py
│       ├── message_service.py
│       ├── announcement_service.py
│       ├── analytics_service.py
│       └── query_service.py
├── test/                     # Test suite
│   ├── __init__.py
│   ├── test_ai_functions.py
│   ├── test_new_ai_functions.py
│   └── test_services_*.py    # Service-specific tests
├── requirements.txt          # Python dependencies
├── pyproject.toml           # Project configuration
├── pytest.ini              # Test configuration
├── Dockerfile               # Docker configuration (empty)
├── docker-compose.yml       # Docker Compose (empty)
└── .gitignore              # Git ignore rules
```

## 🗄 Database Schema

### Core Entities

#### Buildings
- **Primary Key**: `building_id` (String)
- **Attributes**: 30+ properties including address, amenities, operator assignment
- **Relationships**: One-to-many with rooms, tenants

#### Rooms
- **Primary Key**: `room_id` (String)
- **Attributes**: Room details, pricing, amenities, status
- **Relationships**: Belongs to building, can have multiple tenants

#### Tenants
- **Primary Key**: `tenant_id` (String)
- **Attributes**: Personal info, lease details, payment status
- **Relationships**: Belongs to room and building

#### Leads
- **Primary Key**: `lead_id` (String)
- **Attributes**: Contact info, preferences, conversion tracking
- **Relationships**: Can be associated with rooms

#### Operators
- **Primary Key**: `operator_id` (Integer)
- **Attributes**: Staff info, roles, permissions
- **Relationships**: Manages buildings, handles maintenance

### Extended Entities

#### Maintenance Requests
- **Primary Key**: `request_id` (String)
- **Attributes**: Title, description, priority, status
- **Relationships**: Links to room, building, tenant, operator

#### Scheduled Events
- **Primary Key**: `event_id` (String)
- **Attributes**: Event type, timing, participants
- **Relationships**: Can involve rooms, buildings, operators, leads, tenants

#### Documents
- **Primary Key**: `document_id` (String)
- **Attributes**: Document type, content, status
- **Relationships**: Associated with tenants, leads, rooms, buildings

## 🤖 AI Integration

### Gemini API Integration
The system uses Google's Gemini API for natural language processing:

```python
# AI Function Example
def find_buildings_rooms_function(query: str, db: Session) -> Dict[str, Any]:
    """Finds buildings and rooms based on user query using Gemini Function Calling"""
    # Processes natural language queries like:
    # "Find me a room with city view and private bathroom"
    # "Show me affordable rooms under $2000"
```

### AI Functions Registry
- `find_buildings_rooms_function`: Room search with natural language
- `admin_data_query_function`: Administrative data queries
- `schedule_showing_function`: Automated showing scheduling
- `filter_rooms_function`: Advanced room filtering
- `schedule_event_function`: Event scheduling
- `process_maintenance_request_function`: Maintenance workflow
- `generate_insights_function`: Analytics and insights
- `create_communication_function`: Automated communications
- `generate_document_function`: Document generation
- `manage_checklist_function`: Checklist management

## 🔌 API Endpoints

### Core Resources
- **Buildings**: `/buildings/` - CRUD operations for buildings
- **Rooms**: `/rooms/` - Room management and availability
- **Tenants**: `/tenants/` - Tenant lifecycle management
- **Leads**: `/leads/` - Lead tracking and conversion
- **Operators**: `/operators/` - Staff management

### AI-Powered Endpoints
- **Query**: `/query/` - Natural language search interface
- **Analytics**: `/analytics/` - AI-generated insights

### Operational Endpoints
- **Maintenance**: `/maintenance-requests/` - Maintenance workflow
- **Scheduling**: `/scheduled-events/` - Event management
- **Notifications**: `/notifications/` - Communication system
- **Documents**: `/documents/` - Document generation and management

## 🧪 Testing Strategy

### Test Structure
- **Unit Tests**: Service layer testing with mocked dependencies
- **Integration Tests**: Database integration with in-memory SQLite
- **AI Function Tests**: Mocked Gemini API responses

### Test Coverage
- All service functions
- AI function behavior
- Database operations
- Error handling scenarios

### Running Tests
```bash
# Install dependencies
pip install -r requirements.txt

# Set environment variables (required)
export SUPABASE_DB_URL="your_database_url"
export SUPABASE_DB_PASSWORD="your_password"
export GEMINI_API_KEY="your_gemini_key"

# Run tests
python -m pytest test/ -v
```

## ⚙️ Configuration

### Environment Variables
```bash
# Database Configuration
SUPABASE_DB_URL=postgresql://user:password@host:port/database
SUPABASE_DB_PASSWORD=your_database_password

# AI Configuration
GEMINI_API_KEY=your_gemini_api_key
```

### Configuration Files
- `pyproject.toml`: Project metadata and dependencies
- `pytest.ini`: Test configuration
- `.env`: Environment variables (not included in repo)

## 🚀 Getting Started

### Prerequisites
- Python 3.11+
- PostgreSQL database (Supabase recommended)
- Google Gemini API key

### Installation
```bash
# Clone the repository
git clone <repository-url>
cd homewiz-backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env  # Create this file
# Edit .env with your configuration

# Run database migrations (if available)
# python -m alembic upgrade head

# Seed the database
python app/db/scripts/seed_db.py

# Start the server
uvicorn app.main:app --reload
```

### API Documentation
Once running, access the interactive API documentation at:
- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## 📊 Project Assessment

### Strengths (8.5/10)
✅ **Excellent Architecture**: Clean separation of concerns, proper layering
✅ **Comprehensive Domain**: Rich data models reflecting real-world complexity
✅ **AI Innovation**: Creative integration of Gemini API for natural language processing
✅ **Professional Code**: Consistent patterns, proper dependency injection
✅ **Robust Testing**: Comprehensive test coverage with proper mocking

### Areas for Improvement (6/10)
❌ **Infrastructure Gaps**: Empty Docker files, missing middleware
❌ **Configuration Issues**: Hard dependencies on environment variables
❌ **Security Missing**: No authentication, authorization, or input validation
❌ **Production Readiness**: Missing monitoring, logging, error handling
❌ **Documentation**: Limited setup instructions and API examples

### Code Quality (8/10)
✅ **Clean Code**: Readable, well-organized, consistent naming
✅ **Type Safety**: Good use of Pydantic for validation
✅ **Error Handling**: Basic error handling in place
❌ **Type Hints**: Inconsistent type annotations
❌ **Documentation**: Missing docstrings and inline comments

### Innovation (9/10)
✅ **AI Integration**: Sophisticated use of function calling with Gemini
✅ **Modern Stack**: Current versions of FastAPI, SQLAlchemy, Pydantic
✅ **Scalable Design**: Well-structured for future expansion
✅ **Business Logic**: Realistic property management workflows

## 🎯 Recommendations

### Immediate Priorities (Week 1)
1. **Fix Test Environment**: Create test configuration without external dependencies
2. **Complete Docker Setup**: Implement Dockerfile and docker-compose.yml
3. **Add Basic Auth**: JWT-based authentication middleware
4. **Environment Management**: Proper configuration with defaults

### Short-term Goals (Month 1)
1. **Database Migrations**: Implement Alembic for schema management
2. **API Documentation**: Complete OpenAPI specs with examples
3. **Error Handling**: Centralized exception handling and logging
4. **Security Hardening**: Input validation, CORS, rate limiting

### Medium-term Objectives (Quarter 1)
1. **Performance Optimization**: Caching, query optimization, async operations
2. **Monitoring**: Metrics, health checks, observability
3. **Advanced AI Features**: Enhanced query processing and insights
4. **Integration Testing**: End-to-end API testing

## 📞 Support & Maintenance

### Code Quality Tools (Recommended)
```bash
# Code formatting
pip install black isort

# Type checking
pip install mypy

# Linting
pip install flake8

# Pre-commit hooks
pip install pre-commit
```

### Monitoring & Logging (To Implement)
- **Application Monitoring**: Prometheus + Grafana
- **Error Tracking**: Sentry integration
- **API Monitoring**: Request/response logging
- **Performance Metrics**: Database query optimization

## 🏆 Conclusion

HomeWiz Backend is a **high-quality, well-architected project** that demonstrates strong software engineering principles. The AI integration is particularly impressive and shows innovative thinking. While there are gaps in infrastructure and production-readiness, the core foundation is solid and the codebase is maintainable and extensible.

**Overall Rating**: 8/10
**Recommendation**: Continue development with focus on infrastructure completion and production-ready features. This project has strong commercial potential.

## 🔧 Development Workflow

### Code Standards
```python
# Example of proper service function structure
def create_building(db: Session, building: BuildingCreate) -> models.Building:
    """
    Creates a new building in the database.

    Args:
        db: Database session
        building: Building creation data

    Returns:
        Created building instance

    Raises:
        ValueError: If building data is invalid
    """
    db_building = models.Building(**building.dict())
    db.add(db_building)
    db.commit()
    db.refresh(db_building)
    return db_building
```

### Git Workflow (Recommended)
```bash
# Feature development
git checkout -b feature/new-feature
git commit -m "feat: add new feature"
git push origin feature/new-feature

# Create pull request for review
# Merge after approval
```

### Database Operations
```python
# Database seeding
python app/db/scripts/seed_db.py

# Check database tables
python app/db/scripts/check_tables.py

# Manual database connection test
python app/db/connection.py
```

## 🐛 Troubleshooting

### Common Issues

#### 1. Environment Variable Errors
```bash
# Error: SUPABASE_DB_URL not set
# Solution: Create .env file with required variables
echo "SUPABASE_DB_URL=your_url_here" > .env
echo "GEMINI_API_KEY=your_key_here" >> .env
```

#### 2. Test Failures
```bash
# Error: OSError: SUPABASE_DB_URL not set
# Solution: Tests need environment variables or mocking
export SUPABASE_DB_URL="sqlite:///:memory:"
export GEMINI_API_KEY="test_key"
```

#### 3. Import Errors
```bash
# Error: ModuleNotFoundError
# Solution: Install dependencies and check Python path
pip install -r requirements.txt
export PYTHONPATH="${PYTHONPATH}:$(pwd)"
```

### Debug Mode
```python
# Enable debug logging
import logging
logging.basicConfig(level=logging.DEBUG)

# Run with debug
uvicorn app.main:app --reload --log-level debug
```

## 📈 Performance Considerations

### Database Optimization
```python
# Add database indexes (recommended)
# In models.py
class Room(Base):
    __tablename__ = "rooms"

    room_id = Column(String, primary_key=True, index=True)
    building_id = Column(String, ForeignKey("buildings.building_id"), index=True)
    status = Column(String, default="AVAILABLE", index=True)  # Add index
    private_room_rent = Column(Float, index=True)  # Add index for price queries
```

### Caching Strategy
```python
# Redis caching (to implement)
from functools import lru_cache
import redis

@lru_cache(maxsize=100)
def get_building_cache(building_id: str):
    # Cached building lookup
    pass
```

### Async Operations
```python
# Convert to async for better performance
async def create_building_async(db: AsyncSession, building: BuildingCreate):
    # Async database operations
    pass
```

## 🔒 Security Implementation Guide

### Authentication Middleware
```python
# app/middleware/auth.py (to implement)
from fastapi import HTTPException, Depends
from fastapi.security import HTTPBearer
import jwt

security = HTTPBearer()

async def verify_token(token: str = Depends(security)):
    try:
        payload = jwt.decode(token.credentials, SECRET_KEY, algorithms=["HS256"])
        return payload
    except jwt.ExpiredSignatureError:
        raise HTTPException(status_code=401, detail="Token expired")
```

### Input Validation
```python
# Enhanced Pydantic models with validation
from pydantic import validator, EmailStr

class BuildingCreate(BaseModel):
    building_name: str
    email: EmailStr  # Email validation

    @validator('building_name')
    def validate_name(cls, v):
        if len(v) < 3:
            raise ValueError('Building name must be at least 3 characters')
        return v
```

### Rate Limiting
```python
# app/middleware/rate_limit.py (to implement)
from slowapi import Limiter, _rate_limit_exceeded_handler
from slowapi.util import get_remote_address

limiter = Limiter(key_func=get_remote_address)

@app.route("/api/search")
@limiter.limit("10/minute")
def search_rooms():
    # Rate limited endpoint
    pass
```

## 📊 Monitoring & Analytics

### Health Checks
```python
# app/endpoints/health.py (to implement)
@router.get("/health")
async def health_check():
    return {
        "status": "healthy",
        "timestamp": datetime.utcnow(),
        "version": "0.1.0"
    }
```

### Metrics Collection
```python
# Prometheus metrics (to implement)
from prometheus_client import Counter, Histogram

REQUEST_COUNT = Counter('requests_total', 'Total requests', ['method', 'endpoint'])
REQUEST_DURATION = Histogram('request_duration_seconds', 'Request duration')
```

### Error Tracking
```python
# Sentry integration (to implement)
import sentry_sdk
from sentry_sdk.integrations.fastapi import FastApiIntegration

sentry_sdk.init(
    dsn="your-sentry-dsn",
    integrations=[FastApiIntegration()],
)
```

## 🚀 Deployment Guide

### Docker Deployment
```dockerfile
# Dockerfile (to complete)
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

```yaml
# docker-compose.yml (to complete)
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:8000"
    environment:
      - SUPABASE_DB_URL=${SUPABASE_DB_URL}
      - GEMINI_API_KEY=${GEMINI_API_KEY}
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: homewiz
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

### Production Checklist
- [ ] Environment variables configured
- [ ] Database migrations applied
- [ ] SSL certificates installed
- [ ] Monitoring setup (Prometheus/Grafana)
- [ ] Error tracking configured (Sentry)
- [ ] Backup strategy implemented
- [ ] Load balancer configured
- [ ] Rate limiting enabled
- [ ] Security headers configured

## 🤝 Contributing Guidelines

### Pull Request Process
1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

### Code Review Checklist
- [ ] Code follows project style guidelines
- [ ] Tests added for new functionality
- [ ] Documentation updated
- [ ] No breaking changes without migration path
- [ ] Security considerations addressed

### Issue Templates
```markdown
## Bug Report
**Describe the bug**
A clear description of the bug.

**To Reproduce**
Steps to reproduce the behavior.

**Expected behavior**
What you expected to happen.

**Environment**
- OS: [e.g. macOS]
- Python version: [e.g. 3.11]
- FastAPI version: [e.g. 0.115.11]
```

## 📚 Additional Resources

### Learning Resources
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [SQLAlchemy 2.0 Tutorial](https://docs.sqlalchemy.org/en/20/tutorial/)
- [Pydantic Documentation](https://docs.pydantic.dev/)
- [Google Gemini API](https://ai.google.dev/docs)

### Similar Projects
- Property management systems
- Real estate platforms
- Rental marketplace backends

### Community
- FastAPI Discord
- Python Property Management Groups
- AI Integration Communities

---

*Last Updated: June 2025*
*Version: 0.1*
*Author: AI Analysis*
*Document Type: Comprehensive Technical Documentation*
