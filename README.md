# 📊 Statistical Visualization Platform - Backend

PostgreSQL-backed REST API serving **9.1 million government records** with lightning-fast queries.

## 🚀 Features

- ✅ **9.1M Records**: Complete dataset from data.gov.in APIs
- ✅ **PostgreSQL Database**: Enterprise-grade data storage
- ✅ **Fast Queries**: <500ms response time using materialized views
- ✅ **RESTful API**: Clean endpoints for data access
- ✅ **Scalable Architecture**: Ready for production deployment

## 📊 Data Sources

- **Biometrics**: 5.5M records (fingerprint, iris updates)
- **Demographics**: 2.4M records (age groups, gender distribution)
- **Enrolment**: 1.2M records (enrolment centers, daily stats)

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: PostgreSQL 15+
- **API Client**: node-fetch
- **Compression**: gzip

## 📋 Prerequisites

- Node.js 16+ ([Download](https://nodejs.org/))
- PostgreSQL 15+ ([Download](https://www.postgresql.org/download/))
- data.gov.in API key ([Get here](https://data.gov.in/))

## 🚀 Quick Start

### 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/statistical-viz-backend.git
cd statistical-viz-backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment

```bash
# Copy example environment file
cp .env.example .env

# Edit .env and add your credentials
# DB_PASSWORD=your_postgres_password
# API_KEY=your_data_gov_in_api_key
```

### 4. Create Database

```bash
# Using psql
psql -U postgres -c "CREATE DATABASE statistical_viz"

# Or using pgAdmin GUI
```

### 5. Setup Schema

```bash
npm run setup
```

This creates:
- 3 tables (biometrics, demographics, enrolment)
- Indexes for fast queries
- Materialized views for aggregations

### 6. Import Data (Optional)

**⚠️ Takes 2-3 hours for full dataset**

```bash
npm run fetch
```

Or import from backup:
```bash
psql -U postgres statistical_viz < backup.sql
```

### 7. Start Server

```bash
npm start
```

Server runs on `http://localhost:3001`

## 📡 API Endpoints

### GET `/api/data`
Complete aggregated dataset
```json
{
  "summary": { "totalRecords": 9100000, ... },
  "monthly": [...],
  "districts": [...]
}
```

### GET `/api/summary`
Quick statistics
```json
{
  "totalRecords": 9100000,
  "bioRecords": 5512637,
  "demoRecords": 2375882,
  "enrolRecords": 1208727
}
```

### GET `/api/monthly`
Month-wise aggregation

### GET `/api/districts?state=Maharashtra&limit=50`
District data with filters

### POST `/api/refresh-views`
Refresh materialized views

## 🗄️ Database Schema

### Tables

- `biometrics` (5.5M records)
- `demographics` (2.4M records)
- `enrolment` (1.2M records)

### Indexes

- Date-based indexes for time-series queries
- State/district indexes for geographical filtering
- Composite indexes for complex queries

### Materialized Views

- `monthly_summary` - Pre-aggregated monthly data
- `district_summary` - Pre-aggregated district data

## ⚡ Performance

| Query | Records | Response Time |
|-------|---------|---------------|
| Monthly Summary | 9.1M | <50ms |
| District Summary | 9.1M | <100ms |
| Top 100 Districts | 9.1M | <200ms |

## 🚀 Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed deployment instructions to:

- **Render** (Recommended - Free tier)
- **Railway** (Easy & fast)
- **Heroku** (Popular choice)
- **DigitalOcean** (Professional)

Quick deploy to Render:

1. Push to GitHub
2. Create Render account
3. Create PostgreSQL database
4. Create web service from GitHub
5. Set environment variables
6. Deploy!

## 🔧 Maintenance

### Refresh Materialized Views

```bash
curl -X POST http://localhost:3001/api/refresh-views
```

### Backup Database

```bash
pg_dump -U postgres statistical_viz > backup.sql
```

### Check Database Size

```sql
SELECT pg_size_pretty(pg_database_size('statistical_viz'));
```

## 📁 Project Structure

```
.
├── server-db.js           # Express API server
├── setup-database.js      # Database schema setup
├── fetch-all-data.js      # Data import script
├── package.json           # Dependencies
├── .env.example           # Environment template
├── .gitignore            # Git ignore rules
├── README.md             # This file
└── DEPLOYMENT.md         # Deployment guide
```

## 🐛 Troubleshooting

### Connection Refused
- Check PostgreSQL is running
- Verify port 5432 is open
- Check `.env` credentials

### Out of Memory
- Increase PostgreSQL memory settings
- Reduce batch size in `fetch-all-data.js`

### Slow Queries
- Run `ANALYZE` on tables
- Refresh materialized views
- Check index usage

## 📄 License

MIT License - feel free to use for your projects

## 🤝 Contributing

Contributions welcome! Please open an issue or submit a PR.

## 📞 Support

For issues and questions:
- Open a GitHub issue
- Check [DEPLOYMENT.md](DEPLOYMENT.md) for deployment help
- See [PostgreSQL docs](https://www.postgresql.org/docs/)

## 🎉 Acknowledgments

- Data source: [data.gov.in](https://data.gov.in/)
- Built with PostgreSQL, Express, and Node.js

---

**Built with ❤️ for handling massive government datasets efficiently**
