Django Property Listings with Redis Caching
This project is a Django-based property listing application that demonstrates multi-level caching with Redis. The application uses Dockerized PostgreSQL for persistent storage and Redis for caching to reduce database load and improve response times.
Features
•	Property Listings (title, description, price, location, created_at)
•	Multi-level caching:
  - View-level caching (@cache_page) for 15 minutes
  - Low-level queryset caching with Redis (1 hour)
•	Cache invalidation using Django signals
•	Cache metrics analysis (hits, misses, hit ratio)
•	Dockerized services for PostgreSQL and Redis
Tech Stack
•	Django – web framework
•	PostgreSQL – relational database
•	Redis – in-memory cache
•	Docker + docker-compose – containerized services
•	django-redis – Redis cache backend for Django
•	psycopg2-binary – PostgreSQL adapter
Getting Started
1. Clone the Repository
git clone https://github.com/<your-username>/alx-backend-caching_property_listings.git
cd alx-backend-caching_property_listings
2. Start Services with Docker
docker-compose up -d

This runs:
- PostgreSQL (on port 5432)
- Redis (on port 6379)
3. Install Dependencies
pip install -r requirements.txt
4. Apply Migrations
python manage.py migrate
5. Run the Server
python manage.py runserver

Visit http://127.0.0.1:8000/properties/
Project Structure
alx-backend-caching_property_listings/
│── docker-compose.yml
│── manage.py
├── alx_backend_caching_property_listings/
│   └── settings.py, urls.py
├── properties/
│   ├── models.py, views.py, utils.py, signals.py, urls.py, apps.py
└── templates/properties/property_list.html
Caching Workflows
1. View-Level Caching
@cache_page(60 * 15)
def property_list(request):
    ...
2. Low-Level Queryset Caching
from django.core.cache import cache
properties = cache.get('all_properties')
3. Cache Invalidation (via Signals)
@receiver([post_save, post_delete], sender=Property)
def clear_property_cache(sender, **kwargs):
    cache.delete('all_properties')
4. Cache Metrics
{
  'hits': 120,
  'misses': 30,
  'hit_ratio': 0.8
}
Assessment Notes
•	Core files included (settings.py, docker-compose.yml, models.py, views.py, utils.py, signals.py)
•	Implements all mandatory tasks (0–4)
•	Ready for manual review
Author
GitHub: https://github.com/derickmokua

