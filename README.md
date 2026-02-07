# POS
POINT OF SALE
# Universal Configurable POS System

> **Enterprise-Grade, Metadata-Driven Point of Sale Platform**  
> Adaptable to any business type through configuration, not code changes.

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18-blue.svg)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🎯 Vision

A **zero-code-change POS platform** that adapts to retail stores, restaurants, service businesses, and any other business model through pure configuration and metadata management.

---

## ✨ Core Features

### 🔧 Configuration-Driven Architecture
- **Business Type Agnostic**: Retail, Restaurant, Salon, Auto Service, Healthcare, etc.
- **Dynamic UI Generation**: Forms, tables, and workflows generated from metadata
- **Custom Field Engine**: Add unlimited custom fields without schema changes
- **Workflow Engine**: Configure approval chains, notifications, and business rules
- **Multi-tenant Ready**: Isolated data with shared infrastructure

### 💼 Business Capabilities
- **Sales & Transactions**
  - Multi-payment processing (Cash, Card, Digital Wallets, Split payments)
  - Refunds, exchanges, and returns management
  - Layaway and installment plans
  - Gift cards and store credit
  
- **Inventory Management**
  - Multi-location warehouse support
  - Stock transfers and adjustments
  - Barcode/QR code scanning
  - Automated reorder points
  - Batch and serial number tracking
  - Expiry date management
  
- **Customer Relationship Management**
  - Customer profiles and purchase history
  - Loyalty programs (points, tiers, rewards)
  - Personalized pricing and discounts
  - Customer groups and segmentation
  
- **Product Catalog**
  - Unlimited product variants (size, color, etc.)
  - Bundle and combo products
  - Digital products and services
  - Recipe/BOM management for manufacturing
  
- **Pricing & Promotions**
  - Dynamic pricing rules
  - Time-based promotions
  - Volume discounts
  - Customer-specific pricing
  - Tax configuration (single/multiple, inclusive/exclusive)
  
- **Reporting & Analytics**
  - Real-time sales dashboard
  - Inventory reports
  - Customer analytics
  - Financial reports
  - Custom report builder

### 🏗️ Technical Capabilities
- **RESTful API**: Complete API-first design
- **Real-time Updates**: WebSocket support for live data
- **Offline Mode**: Progressive Web App with local storage
- **Role-Based Access Control**: Granular permissions system
- **Audit Trail**: Complete change tracking
- **Multi-currency & Multi-language**: I18n support
- **Import/Export**: CSV, Excel, JSON data migration
- **Extensible Plugin System**: Custom modules without core changes

---

## 🏛️ Architecture Overview

### System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Presentation Layer                       │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │   React     │  │  Mobile PWA  │  │  Admin Portal    │   │
│  │   POS UI    │  │              │  │                  │   │
│  └─────────────┘  └──────────────┘  └──────────────────┘   │
└────────────────────────────┬────────────────────────────────┘
                             │ REST API / WebSocket
┌────────────────────────────┴────────────────────────────────┐
│                     Application Layer                        │
│  ┌──────────────────────────────────────────────────────┐   │
│  │              Spring Boot Backend                     │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │  API Gateway  │  Security  │  Metadata Engine        │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │  Business Services Layer                             │   │
│  │  • Transaction Service    • Inventory Service        │   │
│  │  • Customer Service       • Pricing Service          │   │
│  │  • Reporting Service      • Configuration Service    │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │  Domain Layer (DDD)                                  │   │
│  │  • Entities  • Value Objects  • Aggregates           │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │  Data Access Layer (JPA/Hibernate)                   │   │
│  └──────────────────────────────────────────────────────┘   │
└────────────────────────────┬────────────────────────────────┘
                             │ JDBC
┌────────────────────────────┴────────────────────────────────┐
│                     Data Layer                               │
│  ┌──────────────────────────────────────────────────────┐   │
│  │              PostgreSQL Database                     │   │
│  ├──────────────────────────────────────────────────────┤   │
│  │  • Multi-tenant schema (tenant_id partitioning)      │   │
│  │  • JSONB for flexible metadata storage               │   │
│  │  • Full-text search with GIN indexes                 │   │
│  │  • Materialized views for reporting                  │   │
│  │  • Row-level security for data isolation             │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Metadata-Driven Engine

```
Configuration Files (JSON/YAML)
        ↓
Metadata Repository (Database)
        ↓
Runtime Metadata Engine
        ↓
┌───────────────┬─────────────┬──────────────┐
│  UI Generator │ Validation  │ Business     │
│               │ Rules       │ Logic Engine │
└───────────────┴─────────────┴──────────────┘
        ↓
Dynamic Application Behavior
```

---

## 📊 Database Schema Strategy

### Core Principles
1. **EAV Pattern for Flexibility**: Entity-Attribute-Value for custom fields
2. **JSONB for Metadata**: PostgreSQL JSONB columns for configuration
3. **Multi-tenant Isolation**: `tenant_id` on all tables with RLS policies
4. **Temporal Data**: Effective dating for pricing, configurations
5. **Soft Deletes**: Audit-friendly deletion with `deleted_at`

### Key Schema Components

#### Configuration Tables
- `tenants` - Multi-tenant isolation
- `business_types` - Retail, Restaurant, Service, etc.
- `entity_definitions` - Define custom entities (Product, Service, etc.)
- `field_definitions` - Dynamic field configurations
- `ui_layouts` - Screen layouts and forms
- `workflow_definitions` - Business process flows
- `business_rules` - Validation and calculation rules

#### Operational Tables
- `transactions` - All sales transactions
- `transaction_items` - Line items with dynamic attributes
- `products` - Base product catalog
- `product_variants` - SKU-level variants
- `inventory` - Stock levels per location
- `customers` - Customer master data
- `payments` - Payment records
- `pricing_rules` - Dynamic pricing engine

#### Supporting Tables
- `locations` - Stores/warehouses
- `employees` - Staff management
- `tax_configurations` - Tax rules
- `discount_rules` - Promotion engine
- `audit_logs` - Complete audit trail

---

## 🚀 Getting Started

### Prerequisites
- Java 17+
- Node.js 18+
- PostgreSQL 15+
- Maven 3.8+
- Git

### Quick Start with GitHub Codespaces

1. **Fork/Clone this repository**
   ```bash
   git clone https://github.com/yourusername/pos-app.git
   cd pos-app
   ```

2. **Open in Codespaces**
   - Click "Code" → "Codespaces" → "Create codespace on main"
   - Dev container will auto-configure Java, Node, PostgreSQL

3. **Initialize Database**
   ```bash
   cd backend/pos-backend
   mvn flyway:migrate
   ```

4. **Start Backend**
   ```bash
   mvn spring-boot:run
   ```

5. **Start Frontend** (new terminal)
   ```bash
   cd frontend
   npm install
   npm start
   ```

6. **Access Application**
   - Frontend: `http://localhost:3000`
   - Backend API: `http://localhost:8080`
   - API Docs: `http://localhost:8080/swagger-ui.html`

### Local Development Setup

```bash
# 1. Start PostgreSQL
docker run --name pos-postgres \
  -e POSTGRES_DB=posdb \
  -e POSTGRES_USER=posuser \
  -e POSTGRES_PASSWORD=pospassword \
  -p 5432:5432 \
  -d postgres:15

# 2. Backend
cd backend/pos-backend
mvn clean install
mvn spring-boot:run

# 3. Frontend
cd frontend
npm install
npm start
```

---

## 📁 Project Structure

```
pos-app/
├── backend/
│   └── pos-backend/
│       ├── src/
│       │   ├── main/
│       │   │   ├── java/com/posapp/
│       │   │   │   ├── config/           # Spring configurations
│       │   │   │   ├── controller/       # REST endpoints
│       │   │   │   ├── service/          # Business logic
│       │   │   │   ├── repository/       # Data access
│       │   │   │   ├── domain/           # Domain models
│       │   │   │   │   ├── model/        # Entities
│       │   │   │   │   ├── dto/          # Data transfer objects
│       │   │   │   │   └── enums/        # Enumerations
│       │   │   │   ├── metadata/         # Metadata engine
│       │   │   │   ├── security/         # Auth & authorization
│       │   │   │   ├── exception/        # Exception handling
│       │   │   │   └── util/             # Utilities
│       │   │   └── resources/
│       │   │       ├── db/migration/     # Flyway migrations
│       │   │       ├── metadata/         # Business configs
│       │   │       └── application.yml   # App configuration
│       │   └── test/                     # Unit & integration tests
│       └── pom.xml
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/          # Reusable components
│   │   │   ├── pos/             # POS interface
│   │   │   ├── inventory/       # Inventory management
│   │   │   ├── customers/       # Customer management
│   │   │   ├── products/        # Product catalog
│   │   │   ├── reports/         # Reporting UI
│   │   │   └── admin/           # Admin configuration
│   │   ├── hooks/               # Custom React hooks
│   │   ├── services/            # API clients
│   │   ├── context/             # React context
│   │   ├── utils/               # Helper functions
│   │   ├── types/               # TypeScript definitions
│   │   └── App.tsx
│   ├── package.json
│   └── tsconfig.json
│
├── database/
│   ├── migrations/              # SQL migration scripts
│   ├── seeds/                   # Sample data
│   └── schema/                  # Schema documentation
│
├── docs/
│   ├── API.md                   # API documentation
│   ├── CONFIGURATION.md         # Configuration guide
│   ├── DEPLOYMENT.md            # Deployment guide
│   └── ARCHITECTURE.md          # Detailed architecture
│
├── .devcontainer/               # GitHub Codespaces config
├── docker-compose.yml           # Local development stack
└── README.md
```

---

## 🎨 Configuration Examples

### Example: Configuring a Restaurant POS

```json
{
  "businessType": "RESTAURANT",
  "modules": {
    "tableManagement": true,
    "kitchenDisplay": true,
    "onlineOrdering": true,
    "reservations": true
  },
  "transactionFlow": {
    "steps": ["selectTable", "takeOrder", "sendToKitchen", "payment", "closeTable"]
  },
  "customFields": {
    "transaction": [
      {
        "name": "tableNumber",
        "type": "NUMBER",
        "required": true,
        "label": "Table #"
      },
      {
        "name": "specialInstructions",
        "type": "TEXT",
        "label": "Special Instructions"
      }
    ],
    "product": [
      {
        "name": "spicyLevel",
        "type": "SELECT",
        "options": ["Mild", "Medium", "Hot", "Extra Hot"]
      }
    ]
  }
}
```

### Example: Configuring a Retail Store

```json
{
  "businessType": "RETAIL",
  "modules": {
    "barcodeScanning": true,
    "layaway": true,
    "giftRegistry": true,
    "ecommerce": true
  },
  "transactionFlow": {
    "steps": ["scanItems", "applyDiscounts", "payment", "receipt"]
  },
  "customFields": {
    "product": [
      {
        "name": "size",
        "type": "SELECT",
        "options": ["XS", "S", "M", "L", "XL", "XXL"]
      },
      {
        "name": "color",
        "type": "COLOR_PICKER"
      }
    ]
  }
}
```

---

## 🔐 Security Features

- **JWT Authentication**: Stateless token-based auth
- **Role-Based Access Control (RBAC)**: Granular permissions
- **Multi-factor Authentication**: Optional 2FA
- **Data Encryption**: At-rest and in-transit
- **SQL Injection Prevention**: Parameterized queries
- **XSS Protection**: Input sanitization
- **CSRF Protection**: Token validation
- **Rate Limiting**: API throttling
- **Audit Logging**: Complete activity tracking

---

## 📈 Performance Optimization

- **Database Indexing**: Strategic indexes on high-query columns
- **Connection Pooling**: HikariCP for efficient connections
- **Caching**: Redis integration for frequent queries
- **Lazy Loading**: JPA lazy fetch strategies
- **Pagination**: Cursor-based pagination for large datasets
- **Async Processing**: Non-blocking operations
- **CDN Integration**: Static asset delivery
- **Code Splitting**: React lazy loading

---

## 🧪 Testing Strategy

```bash
# Backend
cd backend/pos-backend

# Unit tests
mvn test

# Integration tests
mvn verify

# Code coverage
mvn jacoco:report

# Frontend
cd frontend

# Unit tests
npm test

# E2E tests
npm run test:e2e

# Coverage
npm run test:coverage
```

---

## 🚢 Deployment

### Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up -d

# Scale services
docker-compose up -d --scale backend=3
```

### Cloud Deployment

- **AWS**: ECS/EKS with RDS PostgreSQL
- **Azure**: App Service with Azure Database for PostgreSQL
- **GCP**: Cloud Run with Cloud SQL
- **Kubernetes**: Helm charts included

See [DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed instructions.

---

## 📚 Documentation

- [API Reference](docs/API.md) - Complete API documentation
- [Configuration Guide](docs/CONFIGURATION.md) - How to configure for different business types
- [Architecture Deep Dive](docs/ARCHITECTURE.md) - Detailed technical architecture
- [User Manual](docs/USER_MANUAL.md) - End-user documentation
- [Developer Guide](docs/DEVELOPER_GUIDE.md) - Contributing guidelines

---

## 🗺️ Roadmap

### Phase 1: Core Foundation (Current)
- ✅ Multi-tenant infrastructure
- ✅ Metadata engine
- ✅ Basic transaction processing
- ✅ Product catalog management
- ✅ Customer management

### Phase 2: Advanced Features (Q2 2026)
- ⬜ Advanced reporting & BI
- ⬜ Mobile app (iOS/Android)
- ⬜ Offline-first PWA
- ⬜ Payment gateway integrations
- ⬜ E-commerce integration

### Phase 3: AI & Automation (Q3 2026)
- ⬜ Predictive inventory management
- ⬜ Customer behavior analytics
- ⬜ Dynamic pricing AI
- ⬜ Chatbot support
- ⬜ Voice-activated POS

### Phase 4: Enterprise Features (Q4 2026)
- ⬜ Multi-company consolidation
- ⬜ Advanced franchise management
- ⬜ Supply chain integration
- ⬜ Manufacturing module
- ⬜ Financial accounting integration

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Team & Support

- **Lead Architect**: [Your Name]
- **Documentation**: [Contributor Name]
- **Support Email**: support@posapp.com
- **Discord Community**: [Join our Discord](#)
- **Stack Overflow**: Tag `universal-pos`

---

## 🙏 Acknowledgments

- Spring Boot Team for the excellent framework
- React Team for the powerful UI library
- PostgreSQL Community for the robust database
- All open-source contributors

---

## 📊 Project Status

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Coverage](https://img.shields.io/badge/coverage-85%25-green)
![Version](https://img.shields.io/badge/version-1.0.0--beta-blue)
![Last Commit](https://img.shields.io/badge/last%20commit-today-brightgreen)

---

**Built with ❤️ for businesses worldwide**

*From small retailers to enterprise chains, one platform for all.*
