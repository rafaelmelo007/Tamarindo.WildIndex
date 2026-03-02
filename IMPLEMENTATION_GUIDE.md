# WildIndex — Complete Project & Learning Guide

## Project Overview

A citizen science wildlife platform where users log animal sightings with rich species characteristics — physical traits, behaviors, habitat context, and concerns. Over time, the community builds living species profiles from real-world field observations, all explorable on a public Google Maps interface.

**What makes it different from iNaturalist:** WildIndex is characterization-first. Users don't just log "I saw a capybara" — they describe size, behavior, habitat context, health condition, and concerns. The platform builds searchable, community-sourced species profiles from structured field data.

**Repo:** `https://github.com/rafaelmelo007/Tamarindo.WildIndex`

---

## Learning Path & Resources

You already know Angular and C#/.NET well, so focus on: Ionic/Capacitor for mobile, PostGIS for geospatial, SignalR for real-time, and Google Maps integration.

### Ionic + Capacitor

**"Ionic - Build iOS, Android & Web Apps with Ionic & Angular" by Maximilian Schwarzmüller (Udemy)**
Bestselling Ionic course. Covers components, navigation, native device features (camera, geolocation), storage, auth, and publishing to App Store/Google Play.
→ https://www.udemy.com/course/ionic-2-the-practical-guide-to-building-ios-android-apps/

**"Capacitor Crash Course" by Simon Grimm (Free Udemy)**
Free 5-day course on Capacitor basics.
→ https://www.udemy.com/course/capacitor-crash-course/

**Simon Grimm / Ionic Academy (YouTube)**
Best Ionic-focused YouTube channel. Practical tutorials on Capacitor plugins, offline storage, camera, geolocation.
→ Search: `Simon Grimm Ionic`

**Official Docs:**
- Ionic: https://ionicframework.com/docs
- Capacitor: https://capacitorjs.com/docs

### .NET 8 Web API + PostgreSQL

**"Build ASP.NET Core Web API - Scratch to Finish (.NET 8)" by Sameer Saini (Udemy)**
11,000+ students, 2,000+ 5-star reviews. EF Core, repository pattern, DDD, auth.
→ https://www.udemy.com/course/build-rest-apis-with-aspnet-core-web-api-entity-framework/

**"ASP.NET Core 9 Ultimate Guide" by Trevoir Williams (Udemy)**
Clean Architecture, EF Core, JWT auth, pagination, testing, Azure deployment.
→ https://www.udemy.com/course/new-aspnet-core-8-complete-course/

**".NET 8 Microservices: DDD, CQRS, Vertical/Clean Architecture" (Udemy)**
PostgreSQL integration, EF Core, CQRS with MediatR, Docker.
→ https://www.udemy.com/course/microservices-architecture-and-implementation-on-dotnet/

**Key Docs:**
- EF Core + PostgreSQL: https://www.npgsql.org/efcore/
- NetTopologySuite (PostGIS in .NET): https://github.com/NetTopologySuite/NetTopologySuite
- SignalR: https://learn.microsoft.com/en-us/aspnet/core/signalr/

### Angular (Refresh)

**"Angular - The Complete Guide" by Maximilian Schwarzmüller (Udemy)**
Updated for Angular 19+ with standalone components, signals, and new control flow.
→ https://www.udemy.com/course/the-complete-guide-to-angular-2/

**"Angular Signals" by Joshua Morony (YouTube)**
Deep dive into Angular Signals.
→ Search: `Joshua Morony Angular Signals`

### Google Maps + Geolocation

- @angular/google-maps: https://github.com/angular/components/tree/main/src/google-maps
- Google Maps JS API: https://developers.google.com/maps/documentation/javascript

### AI Species Identification

- iNaturalist API (free, includes CV): https://api.inaturalist.org/v1/docs/
- Google Cloud Vision API: https://cloud.google.com/vision
- GBIF Species API (taxonomy): https://www.gbif.org/developer/species

### Learning Schedule

| Week | Learning Focus | WildIndex Phase |
|---|---|---|
| 1 | Ionic/Capacitor course | — |
| 2 | .NET Web API course + PostGIS setup | Phase 1 (API Foundation) |
| 3 | Angular Signals refresh + Google Maps | Phase 2 (Frontend Core) |
| 4-5 | Build core features | Phase 3 (Species + Sightings) |
| 6 | AI integration + offline mode | Phase 4 (AI + Offline) |
| 7-8 | Mobile build + polish | Phase 5-6 (Mobile + Public Map) |

---

## Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Backend | .NET 8 Web API (C#) | Your expertise, enterprise-grade |
| Database | PostgreSQL 16 + PostGIS 3.4 | Best geospatial DB, spatial indexes |
| ORM | EF Core + Npgsql + NetTopologySuite | Native PostGIS support |
| Real-time | SignalR | Push notifications for nearby sightings |
| Auth | ASP.NET Identity + JWT | Role-based (user/reviewer/admin) |
| Storage | Azure Blob or local filesystem | Photos (original + thumbnails) |
| Search | PostgreSQL full-text + GIN indexes | No extra infrastructure |
| AI | iNaturalist API (v1) → TF Lite (v2) | Species identification from photos |
| Frontend | Angular 18 + Ionic 8 + Capacitor 6 | Shared codebase: web + iOS + Android |
| Maps | Google Maps JS API + @angular/google-maps | Public exploration, clusters, heatmaps |
| Offline | Ionic Storage (IndexedDB) + Background Sync | Field use without connectivity |
| Push | Firebase Cloud Messaging (Capacitor) | Cross-platform push |
| Taxonomy | GBIF Backbone Taxonomy (seeded) | Standard Linnaean classification |

---

## How the System Works

### Sighting Flow

```
1. USER SPOTS ANIMAL → Opens WildIndex (mobile or web)

2. CAPTURE → Takes photo (camera plugin) + GPS auto-captured + timestamp

3. AI SUGGEST → Photo sent to AI → top 3 species suggestions with confidence
   - User picks one, OR marks "unidentified"

4. CHARACTERIZE → Structured form:
   - Physical: estimated size, coloring, markings, body condition
   - Behavior: activity (feeding, resting, moving, vocalizing...)
   - Habitat: environment (near water, forest, urban, grassland...)
   - Concerns: injured, trapped, invasive, unusual location...
   - Notes: free text

5. SUBMIT → Saved (locally if offline, synced when connected)

6. PROCESS → Backend:
   - Stores sighting + photo
   - Updates species profile (aggregates characteristics)
   - Unidentified → routes to review dashboard
   - Rare/endangered → push notification to nearby users
   - Updates public map

7. EXPLORE → Anyone browses map, searches by traits, views species profiles
```

### Species Profile (Community-Built)

```
Capybara (Hydrochoerus hydrochaeris)
├── Taxonomy: Animalia → Chordata → Mammalia → Rodentia → Caviidae
├── Physical (from 847 observations)
│   ├── Size: 100-130cm (avg)
│   ├── Coloring: Brown (94%), Reddish-brown (6%)
│   └── Condition: Healthy (89%), Thin (7%), Injured (4%)
├── Behavior
│   ├── Activity: Diurnal (72%), Crepuscular (23%), Nocturnal (5%)
│   ├── Social: Group (88%), Solitary (12%)
│   └── Common: Grazing (45%), Swimming (28%), Resting (20%)
├── Habitat
│   ├── Near water: 96%
│   ├── Biomes: Wetland (52%), Grassland (28%), Urban (15%)
│   └── Altitude: 0-500m (93%)
├── Conservation: IUCN Least Concern, Stable
├── Seasonality: Breeding peak Oct-Dec
└── Sighting Map: [clustered markers across South America]
```

---

## Project Structure

```
wildindex/
├── src/
│   ├── WildIndex.Api/                    ← .NET 8 Web API
│   │   ├── Program.cs
│   │   ├── appsettings.json
│   │   ├── Controllers/
│   │   │   ├── AuthController.cs
│   │   │   ├── SightingsController.cs
│   │   │   ├── SpeciesController.cs
│   │   │   ├── CharacteristicsController.cs
│   │   │   ├── ReviewController.cs
│   │   │   ├── MapController.cs
│   │   │   ├── SearchController.cs
│   │   │   ├── NotificationsController.cs
│   │   │   └── GamificationController.cs
│   │   ├── Hubs/
│   │   │   └── SightingHub.cs
│   │   └── Middleware/
│   │       ├── ExceptionMiddleware.cs
│   │       └── RateLimitingMiddleware.cs
│   ├── WildIndex.Core/                   ← Domain entities + interfaces
│   │   ├── Entities/
│   │   │   ├── User.cs
│   │   │   ├── Species.cs
│   │   │   ├── Sighting.cs
│   │   │   ├── SightingCharacteristic.cs
│   │   │   ├── CharacteristicDefinition.cs
│   │   │   ├── CharacteristicCategory.cs
│   │   │   ├── SpeciesProfile.cs
│   │   │   ├── Review.cs
│   │   │   ├── Badge.cs
│   │   │   └── UserBadge.cs
│   │   ├── Interfaces/
│   │   │   ├── ISightingRepository.cs
│   │   │   ├── ISpeciesRepository.cs
│   │   │   ├── ICharacteristicsRepository.cs
│   │   │   └── INotificationService.cs
│   │   ├── DTOs/
│   │   │   ├── SightingDto.cs
│   │   │   ├── SpeciesDto.cs
│   │   │   ├── SpeciesProfileDto.cs
│   │   │   ├── CharacteristicDto.cs
│   │   │   ├── SearchDto.cs
│   │   │   └── MapClusterDto.cs
│   │   └── Enums/
│   │       ├── SightingStatus.cs
│   │       ├── ConcernType.cs
│   │       └── ConservationStatus.cs
│   ├── WildIndex.Infrastructure/         ← EF Core, PostGIS, services
│   │   ├── Data/
│   │   │   ├── AppDbContext.cs
│   │   │   ├── Configurations/
│   │   │   └── Migrations/
│   │   ├── Repositories/
│   │   │   ├── SightingRepository.cs
│   │   │   ├── SpeciesRepository.cs
│   │   │   └── CharacteristicsRepository.cs
│   │   ├── Services/
│   │   │   ├── PhotoService.cs
│   │   │   ├── AiIdentificationService.cs
│   │   │   ├── NotificationService.cs
│   │   │   ├── SpeciesProfileService.cs
│   │   │   ├── GamificationService.cs
│   │   │   └── GbifService.cs
│   │   └── Seed/
│   │       ├── TaxonomySeed.cs
│   │       ├── CharacteristicsSeed.cs
│   │       └── ConservationSeed.cs
│   └── WildIndex.Tests/
├── app/                                  ← Angular + Ionic frontend
│   ├── package.json
│   ├── angular.json
│   ├── ionic.config.json
│   ├── capacitor.config.ts
│   └── src/
│       ├── main.ts
│       └── app/
│           ├── app.component.ts
│           ├── app.routes.ts
│           ├── core/
│           │   ├── services/
│           │   │   ├── api.service.ts
│           │   │   ├── auth.service.ts
│           │   │   ├── sighting.service.ts
│           │   │   ├── species.service.ts
│           │   │   ├── search.service.ts
│           │   │   ├── map.service.ts
│           │   │   ├── offline.service.ts
│           │   │   ├── sync.service.ts
│           │   │   ├── notification.service.ts
│           │   │   ├── camera.service.ts
│           │   │   └── geolocation.service.ts
│           │   ├── guards/
│           │   │   └── auth.guard.ts
│           │   ├── interceptors/
│           │   │   ├── auth.interceptor.ts
│           │   │   └── offline.interceptor.ts
│           │   └── models/
│           │       ├── sighting.model.ts
│           │       ├── species.model.ts
│           │       ├── characteristic.model.ts
│           │       └── user.model.ts
│           ├── features/
│           │   ├── auth/
│           │   │   ├── login/
│           │   │   └── register/
│           │   ├── sighting/
│           │   │   ├── new-sighting/
│           │   │   ├── sighting-detail/
│           │   │   └── my-sightings/
│           │   ├── explore/
│           │   │   ├── map/
│           │   │   ├── species-list/
│           │   │   ├── species-detail/
│           │   │   └── search/
│           │   ├── review/
│           │   │   ├── unclassified/
│           │   │   └── review-detail/
│           │   ├── gamification/
│           │   │   ├── badges/
│           │   │   └── leaderboard/
│           │   └── profile/
│           │       └── user-profile/
│           └── shared/
│               ├── components/
│               │   ├── species-autocomplete/
│               │   ├── characteristic-form/
│               │   ├── photo-capture/
│               │   ├── location-picker/
│               │   ├── concern-selector/
│               │   ├── map-cluster/
│               │   ├── species-card/
│               │   ├── sighting-card/
│               │   ├── trait-badge/
│               │   └── offline-indicator/
│               └── pipes/
│                   ├── distance.pipe.ts
│                   └── time-ago.pipe.ts
├── scripts/
│   ├── seed-taxonomy.sh
│   ├── seed-characteristics.sql
│   └── seed-iucn.sh
├── docker-compose.yml
├── Makefile
├── WildIndex.sln
└── README.md
```

---

## File Descriptions

### Backend — WildIndex.Api

**`Controllers/SightingsController.cs`** — CRUD for sightings. POST accepts multipart form with photo + location + species + characteristics. Triggers AI identification if species unknown. Triggers push if rare species. Returns nearby sightings via PostGIS ST_DWithin.

**`Controllers/SpeciesController.cs`** — Species CRUD + profile. GET `/api/species/{id}/profile` returns aggregated community-built profile with characteristic distributions, map data, seasonality, conservation info.

**`Controllers/CharacteristicsController.cs`** — Returns characteristic definitions by category. GET `/api/characteristics/categories` returns full trait taxonomy. Used by frontend to render dynamic forms.

**`Controllers/SearchController.cs`** — The power endpoint. POST `/api/search` accepts structured query: filter by taxonomy, characteristics, location/radius, date range, concerns. Uses PostGIS for spatial, full-text for text, GIN-indexed JSONB for characteristics.

**`Controllers/MapController.cs`** — Optimized map endpoints. GET `/api/map/clusters?bounds=&zoom=` returns clustered markers for viewport. GET `/api/map/heatmap` returns density data. Uses PostGIS ST_ClusterDBSCAN for server-side clustering.

**`Controllers/ReviewController.cs`** — Unclassified species workflow. Lists unidentified sightings, allows reviewers to suggest species, tracks consensus.

**`Controllers/GamificationController.cs`** — Badges, leaderboards, user stats.

**`Hubs/SightingHub.cs`** — SignalR hub. Users subscribe to geographic regions. New sighting or rare species → real-time push.

### Backend — WildIndex.Core

**`Entities/Species.cs`** — Id, CommonName, ScientificName, Kingdom through Genus, TaxonRank, GbifId, IucnStatus, PopulationTrend, ImageUrl, IsVerified.

**`Entities/Sighting.cs`** — Id, ClientId (UUID for dedup), UserId, SpeciesId (nullable for unidentified), Location (PostGIS Point), Latitude, Longitude, Altitude, PhotoPath, ThumbnailPath, Notes, Status, AiSuggestions (JSON), ObservedAt, SyncedAt.

**`Entities/CharacteristicDefinition.cs`** — Id, CategoryId, Name, Description, InputType (select/multiselect/range/text/boolean), Options (JSON), Unit, ApplicableClasses (which taxonomic classes this applies to), SortOrder.

**`Entities/SightingCharacteristic.cs`** — Junction: SightingId, CharacteristicDefinitionId, Value (string).

**`Entities/SpeciesProfile.cs`** — Cached aggregation: SpeciesId, TotalSightings, CharacteristicAggregations (JSONB), SeasonalityData (JSONB), LastComputedAt.

### Backend — WildIndex.Infrastructure

**`Data/AppDbContext.cs`** — EF Core with PostGIS via UseNetTopologySuite(). Spatial indexes on Sighting.Location. GIN indexes on JSONB columns.

**`Services/AiIdentificationService.cs`** — Calls iNaturalist API with photo, returns top species suggestions with confidence. Falls back gracefully if unavailable.

**`Services/SpeciesProfileService.cs`** — Aggregates all sightings for a species. Groups characteristics by definition, computes distributions, calculates seasonality, generates map data.

**`Services/NotificationService.cs`** — Queries users subscribed to geographic area (PostGIS radius on preferences). Sends via SignalR + Firebase Cloud Messaging.

**`Services/GamificationService.cs`** — Awards badges based on rules. Computes leaderboard rankings.

### Frontend — Angular + Ionic

**`features/sighting/new-sighting/`** — Core user flow: (1) Photo via Capacitor Camera, (2) Auto GPS, (3) AI species suggestion, (4) Confirm species or mark unidentified, (5) Dynamic characteristics form, (6) Add concerns, (7) Submit. Offline: stores locally with sync indicator.

**`features/explore/map/`** — Full-screen Google Maps with clustered markers. Filter panel: species, date, characteristics, concerns. Heatmap toggle. Public, no auth.

**`features/explore/search/`** — Advanced search by characteristics. Dynamic filter form. "Brown animal, ~30cm, near water, clicking sounds" → matching species ranked by trait match.

**`features/explore/species-detail/`** — Community-built profile page. Taxonomy, characteristic distribution charts, sighting map, seasonality chart, conservation status, recent sightings, top contributors.

**`features/review/unclassified/`** — Dashboard for reviewers. Unidentified sightings with photos, location, characteristics. Reviewer suggests species. Consensus (3 agree) → classified.

**`core/services/offline.service.ts`** — IndexedDB via Ionic Storage. Queues sightings offline. Stores photos as base64. Tracks sync status.

**`core/services/sync.service.ts`** — Watches network via Capacitor Network plugin. Uploads queued sightings on reconnect. Server rejects duplicates by clientId.

**`shared/components/characteristic-form/`** — Dynamic form. Receives definitions for selected species class. Renders dropdowns, multi-select chips, range sliders, text. Reusable in new-sighting and search.

---

## Database Schema

```sql
CREATE EXTENSION IF NOT EXISTS postgis;

-- Users
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) NOT NULL UNIQUE,
    username VARCHAR(50) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL DEFAULT 'user',
    avatar_url VARCHAR(500),
    location GEOGRAPHY(Point, 4326),
    notification_radius_km INTEGER DEFAULT 50,
    total_sightings INTEGER DEFAULT 0,
    points INTEGER DEFAULT 0,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Taxonomy (seeded from GBIF)
CREATE TABLE species (
    id SERIAL PRIMARY KEY,
    gbif_id INTEGER UNIQUE,
    common_name VARCHAR(255),
    scientific_name VARCHAR(255) NOT NULL,
    kingdom VARCHAR(100),
    phylum VARCHAR(100),
    class VARCHAR(100),
    "order" VARCHAR(100),
    family VARCHAR(100),
    genus VARCHAR(100),
    taxon_rank VARCHAR(50),
    iucn_status VARCHAR(20),
    population_trend VARCHAR(20),
    image_url VARCHAR(500),
    is_verified BOOLEAN DEFAULT true,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Sightings
CREATE TABLE sightings (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    client_id UUID NOT NULL UNIQUE,
    user_id UUID NOT NULL REFERENCES users(id),
    species_id INTEGER REFERENCES species(id),
    location GEOGRAPHY(Point, 4326) NOT NULL,
    latitude DOUBLE PRECISION NOT NULL,
    longitude DOUBLE PRECISION NOT NULL,
    altitude DOUBLE PRECISION,
    photo_path VARCHAR(500),
    thumbnail_path VARCHAR(500),
    notes TEXT,
    status VARCHAR(20) NOT NULL DEFAULT 'pending',
    ai_suggestions JSONB,
    observed_at TIMESTAMPTZ NOT NULL,
    synced_at TIMESTAMPTZ,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Characteristic Definitions
CREATE TABLE characteristic_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    icon VARCHAR(50),
    sort_order INTEGER NOT NULL DEFAULT 0
);

CREATE TABLE characteristic_definitions (
    id SERIAL PRIMARY KEY,
    category_id INTEGER NOT NULL REFERENCES characteristic_categories(id),
    name VARCHAR(100) NOT NULL,
    description TEXT,
    input_type VARCHAR(20) NOT NULL,
    options JSONB,
    unit VARCHAR(20),
    applicable_classes TEXT[],
    sort_order INTEGER NOT NULL DEFAULT 0
);

-- Sighting Characteristics
CREATE TABLE sighting_characteristics (
    id BIGSERIAL PRIMARY KEY,
    sighting_id UUID NOT NULL REFERENCES sightings(id) ON DELETE CASCADE,
    characteristic_id INTEGER NOT NULL REFERENCES characteristic_definitions(id),
    value TEXT NOT NULL,
    UNIQUE(sighting_id, characteristic_id)
);

-- Concerns
CREATE TABLE sighting_concerns (
    id BIGSERIAL PRIMARY KEY,
    sighting_id UUID NOT NULL REFERENCES sightings(id) ON DELETE CASCADE,
    concern_type VARCHAR(50) NOT NULL,
    severity VARCHAR(20) DEFAULT 'moderate',
    description TEXT
);

-- Species Profiles (precomputed)
CREATE TABLE species_profiles (
    id SERIAL PRIMARY KEY,
    species_id INTEGER NOT NULL UNIQUE REFERENCES species(id),
    total_sightings INTEGER DEFAULT 0,
    characteristic_aggregations JSONB,
    seasonality_data JSONB,
    geographic_bounds JSONB,
    last_computed_at TIMESTAMPTZ
);

-- Reviews
CREATE TABLE reviews (
    id SERIAL PRIMARY KEY,
    sighting_id UUID NOT NULL REFERENCES sightings(id),
    reviewer_id UUID NOT NULL REFERENCES users(id),
    suggested_species_id INTEGER REFERENCES species(id),
    confidence VARCHAR(20),
    notes TEXT,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    UNIQUE(sighting_id, reviewer_id)
);

-- Gamification
CREATE TABLE badges (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    icon VARCHAR(50),
    criteria JSONB NOT NULL
);

CREATE TABLE user_badges (
    user_id UUID NOT NULL REFERENCES users(id),
    badge_id INTEGER NOT NULL REFERENCES badges(id),
    earned_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    PRIMARY KEY (user_id, badge_id)
);

-- Notification Subscriptions
CREATE TABLE notification_subscriptions (
    id SERIAL PRIMARY KEY,
    user_id UUID NOT NULL REFERENCES users(id),
    area GEOGRAPHY(Polygon, 4326),
    species_ids INTEGER[],
    notify_rare BOOLEAN DEFAULT true,
    notify_unclassified BOOLEAN DEFAULT false,
    fcm_token VARCHAR(500),
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Spatial Indexes
CREATE INDEX idx_sightings_location ON sightings USING GIST (location);
CREATE INDEX idx_users_location ON users USING GIST (location);
CREATE INDEX idx_subscriptions_area ON notification_subscriptions USING GIST (area);

-- Regular Indexes
CREATE INDEX idx_sightings_species ON sightings(species_id);
CREATE INDEX idx_sightings_user ON sightings(user_id);
CREATE INDEX idx_sightings_status ON sightings(status);
CREATE INDEX idx_sightings_observed ON sightings(observed_at DESC);
CREATE INDEX idx_sighting_chars_sighting ON sighting_characteristics(sighting_id);
CREATE INDEX idx_sighting_chars_char ON sighting_characteristics(characteristic_id);
CREATE INDEX idx_species_class ON species(class);
CREATE INDEX idx_species_scientific ON species(scientific_name);

-- GIN indexes for JSONB
CREATE INDEX idx_profiles_chars ON species_profiles USING GIN (characteristic_aggregations);
CREATE INDEX idx_sightings_ai ON sightings USING GIN (ai_suggestions);
```

## Configuration

### appsettings.json

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=wildindex;Username=wildindex;Password=changeme"
  },
  "Jwt": {
    "Secret": "change-this-to-a-long-random-string",
    "Issuer": "WildIndex",
    "ExpiryHours": 168
  },
  "Storage": {
    "PhotosPath": "./data/photos",
    "ThumbnailSize": 300,
    "MaxPhotoSizeMb": 10
  },
  "AiIdentification": {
    "Provider": "inaturalist",
    "INaturalistApiUrl": "https://api.inaturalist.org/v1",
    "MinConfidence": 0.7
  },
  "Notifications": {
    "FirebaseProjectId": "",
    "FirebaseCredentialPath": ""
  },
  "Gamification": {
    "ReviewConsensusThreshold": 3,
    "PointsPerSighting": 10,
    "PointsPerReview": 5,
    "PointsPerVerifiedId": 25
  },
  "Map": {
    "DefaultClusterRadius": 50,
    "MaxMarkersPerRequest": 500
  }
}
```

### docker-compose.yml

```yaml
version: '3.8'
services:
  db:
    image: postgis/postgis:16-3.4
    environment:
      POSTGRES_DB: wildindex
      POSTGRES_USER: wildindex
      POSTGRES_PASSWORD: changeme
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
  api:
    build: ./src/WildIndex.Api
    ports:
      - "5000:8080"
    depends_on:
      - db
volumes:
  pgdata:
```

### capacitor.config.ts

```typescript
import { CapacitorConfig } from '@capacitor/cli';

const config: CapacitorConfig = {
  appId: 'com.wildindex.app',
  appName: 'WildIndex',
  webDir: 'www',
  server: { androidScheme: 'https' },
  plugins: {
    Camera: { presentationStyle: 'fullScreen' },
    Geolocation: {},
    Network: {},
    PushNotifications: { presentationOptions: ['badge', 'sound', 'alert'] },
    Storage: {}
  }
};
export default config;
```

---

## API Surface

### Auth
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/auth/register | Create account |
| POST | /api/auth/login | Returns JWT |
| GET | /api/auth/me | Current user + stats |

### Sightings
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/sightings | Create (multipart) |
| GET | /api/sightings/{id} | Detail |
| GET | /api/sightings/mine | User's sightings |
| GET | /api/sightings/nearby?lat=&lng=&radius= | PostGIS nearby |
| POST | /api/sightings/sync | Batch offline sync |

### Species
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/species | List (paginated) |
| GET | /api/species/{id} | Detail |
| GET | /api/species/{id}/profile | Community profile |
| GET | /api/species/autocomplete?q= | Autocomplete |

### Characteristics
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/characteristics/categories | All categories |
| GET | /api/characteristics/for-class/{class} | Traits for class |

### Search
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/search | Multi-filter search |
| GET | /api/search/suggestions?q= | Quick suggestions |

### Map
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/map/clusters?bounds=&zoom= | Clustered markers |
| GET | /api/map/heatmap?species= | Density data |
| GET | /api/map/species-distribution/{id} | One species map |

### Review
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/review/unclassified | Queue |
| POST | /api/review/{sightingId} | Submit suggestion |

### AI
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/ai/identify | Photo to suggestions |

### Gamification
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/gamification/leaderboard | Top contributors |
| GET | /api/gamification/badges | Badges + progress |

### Real-time (SignalR)
| Hub | Event | Description |
|---|---|---|
| /hubs/sightings | NewSighting | New in subscribed area |
| /hubs/sightings | RareSpecies | Rare species nearby |
| /hubs/sightings | NewReview | Review on your sighting |

---

## Species Characteristics System

### Categories

```
Physical
  Body Size: select [Tiny (<5cm), Small (5-20cm), Medium (20-60cm), Large (60-150cm), Very Large (>150cm)]
  Estimated Weight: range, unit kg
  Primary Coloring: multi_select [Black, Brown, White, Gray, Red, Orange, Yellow, Green, Blue, Spotted, Striped]
  Body Condition: select [Healthy, Thin, Injured, Sick]
  Distinctive Markings: text
  Life Stage: select [Juvenile, Subadult, Adult, Elder]

Behavior
  Activity Period: select [Diurnal, Nocturnal, Crepuscular]
  Social Structure: select [Solitary, Pair, Small Group, Large Group]
  Observed Activity: multi_select [Feeding, Resting, Moving, Swimming, Flying, Vocalizing, Mating, Nesting, Hunting, Playing]
  Human Reaction: select [Aggressive, Wary, Indifferent, Curious, Tolerant]
  Interaction With Other Species: text

Habitat
  Primary Environment: select [Forest, Grassland, Wetland, Desert, Mountain, Coastal, Urban, Agricultural, Freshwater, Marine]
  Near Water: boolean
  Canopy Level: select [Ground, Understory, Canopy, Above Canopy, Underground, Underwater]
  Substrate: select [Soil, Rock, Sand, Mud, Vegetation, Water, Snow/Ice]
  Estimated Altitude: range 0-6000, unit m

Reproduction
  Reproductive Activity: select [None, Courting, Mating, Nesting, Carrying Young, With Offspring]
  Offspring Count: range
  Nest Type: select [Burrow, Tree Cavity, Ground Nest, Platform, None Observed]

Concerns
  Concern Type: multi_select [Injured, Trapped, Dead, Invasive, Unusual Location, Habitat Destruction, Pollution, Road Kill, Human Conflict]
  Severity: select [Low, Moderate, High, Critical]
  Action Taken: text
```

### Search by Characteristics Example

```sql
-- "Find nocturnal mammals near water in RS"
SELECT DISTINCT sp.common_name, sp.scientific_name
FROM species sp
JOIN sightings s ON s.species_id = sp.id
JOIN sighting_characteristics sc1 ON sc1.sighting_id = s.id
JOIN sighting_characteristics sc2 ON sc2.sighting_id = s.id
WHERE sp.class = 'Mammalia'
  AND sc1.characteristic_id = 7 AND sc1.value = 'Nocturnal'
  AND sc2.characteristic_id = 12 AND sc2.value = 'true'
  AND ST_DWithin(s.location,
    ST_GeogFromText('SRID=4326;POINT(-51.23 -30.03)'), 200000);
```

---

## AI Species Identification

### v1: iNaturalist API

```
POST https://api.inaturalist.org/v1/computervision/score_image
Body: multipart with image
Response: [{taxon: {id, name, preferred_common_name}, combined_score: 0.92}, ...]
```

Map iNaturalist taxon IDs to GBIF-seeded species via scientific name.

### v2: On-Device TensorFlow Lite (Future)

Bundle TFLite model for offline AI. iNaturalist competition dataset from Kaggle. On-device inference without connectivity.

---

## Offline Mode & Sync

### Storage

```typescript
interface OfflineSighting {
  clientId: string;          // UUID on device
  photo: string;             // base64
  latitude: number;
  longitude: number;
  speciesId?: number;
  characteristics: {id: number, value: string}[];
  concerns: {type: string, severity: string}[];
  notes: string;
  observedAt: string;
  syncStatus: 'pending' | 'syncing' | 'synced' | 'failed';
}
```

### Sync Flow

1. Network plugin detects connectivity
2. Read all pending sightings from IndexedDB
3. Upload photo first, then POST sighting
4. Server uses clientId for idempotency
5. Success: mark synced. Failure: mark failed, retry next cycle
6. Show progress in UI

---

## Implementation Tasks (57 tasks, ~44 days)

### Phase 1 — API Foundation (Days 1-5)
1. Create .NET solution (Api, Core, Infrastructure, Tests)
2. Set up PostgreSQL + PostGIS (Docker)
3. Implement AppDbContext with PostGIS (NetTopologySuite)
4. Write EF Core configurations + migrations
5. Seed taxonomy from GBIF backbone
6. Seed characteristic definitions
7. Implement auth (ASP.NET Identity + JWT)
8. Implement Species CRUD + autocomplete

### Phase 2 — Sightings API (Days 6-10)
9. Photo upload service (resize, thumbnail)
10. Sighting CRUD with PostGIS location
11. Characteristics submission per sighting
12. Concerns tracking
13. Nearby sightings query (ST_DWithin)
14. AI identification service (iNaturalist API)
15. Integration tests for spatial queries

### Phase 3 — Frontend Core (Days 11-16)
16. Scaffold Angular + Ionic project
17. Auth pages (login, register)
18. New-sighting flow (camera, GPS, AI, species, traits, submit)
19. Dynamic characteristic-form component
20. My-sightings page
21. Sighting-detail page
22. Configure Capacitor for Android + iOS

### Phase 4 — Species Profiles & Search (Days 17-22)
23. SpeciesProfileService (aggregate characteristics)
24. Species-detail page with profile charts
25. Search endpoint (trait + location + taxonomy)
26. Search page with dynamic filter form
27. Full-text search with PostgreSQL GIN indexes
28. Species-list page with filters

### Phase 5 — Public Map (Days 23-27)
29. Google Maps in explore/map page
30. Server-side clustering (MapController)
31. Marker clusters + click-to-zoom
32. Heatmap layer toggle
33. Filter panel (species, date, characteristics)
34. Public access (no auth required)

### Phase 6 — Offline + Notifications (Days 28-32)
35. offline.service.ts (IndexedDB storage)
36. sync.service.ts (background sync)
37. offline.interceptor.ts (queue requests offline)
38. Offline indicator component
39. SignalR hub + notification service
40. Firebase Cloud Messaging setup
41. Push notification handling (Capacitor)
42. Notification subscription UI

### Phase 7 — Review + Gamification (Days 33-37)
43. Unclassified dashboard
44. Review submission + consensus logic
45. Badge definitions + award logic
46. Leaderboard endpoint + page
47. Badges page + user progress
48. Points calculation per action

### Phase 8 — Mobile + Polish (Days 38-44)
49. Build Android APK (Capacitor)
50. Build iOS IPA (Capacitor)
51. Test camera + GPS on real devices
52. Optimize photo upload (compress before send)
53. Input validation on all endpoints
54. Error handling audit
55. Rate limiting middleware
56. Write README.md
57. End-to-end test: account, sighting, sync, verify on map

---

## .NET Dependencies (NuGet)

```
Microsoft.AspNetCore.Authentication.JwtBearer
Microsoft.AspNetCore.Identity.EntityFrameworkCore
Microsoft.AspNetCore.SignalR
Npgsql.EntityFrameworkCore.PostgreSQL
Npgsql.EntityFrameworkCore.PostgreSQL.NetTopologySuite
NetTopologySuite
NetTopologySuite.IO.GeoJSON
SixLabors.ImageSharp
FluentValidation.AspNetCore
Serilog.AspNetCore
Swashbuckle.AspNetCore
AutoMapper
FirebaseAdmin
```

## Node/Angular Packages

```
@angular/core, @angular/router, @angular/forms
@ionic/angular
@capacitor/core, @capacitor/cli
@capacitor/camera, @capacitor/geolocation
@capacitor/network, @capacitor/push-notifications, @capacitor/storage
@angular/google-maps
@microsoft/signalr
chart.js, ng2-charts
tailwindcss
```

---

## Architecture Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Database | PostgreSQL + PostGIS | Native geospatial queries and indexes |
| ORM | EF Core + NetTopologySuite | PostGIS types map to C# geometry |
| Mobile | Ionic + Capacitor | Shared Angular codebase web/iOS/Android |
| Characteristics | EAV with typed definitions | Add new traits without schema changes |
| Search | PostgreSQL full-text + GIN | No Elasticsearch for v1 |
| AI (v1) | iNaturalist API | Free, millions of training photos |
| Offline | IndexedDB + clientId dedup | Append-only makes sync simple |
| Map clustering | Server-side PostGIS | Handles millions of markers |
| Real-time | SignalR + FCM | WebSocket + background push |
| Profiles | Precomputed JSONB | Fast reads, recompute on demand |
| Taxonomy | GBIF Backbone seed | 2.3M+ species, standard, free |
| Gamification | Rule-based badges + points | Drives engagement simply |

---

## Quick Reference Links

### Backend
- ASP.NET Core: https://learn.microsoft.com/en-us/aspnet/core/
- EF Core: https://learn.microsoft.com/en-us/ef/core/
- Npgsql PostGIS: https://www.npgsql.org/efcore/mapping/nts.html
- SignalR: https://learn.microsoft.com/en-us/aspnet/core/signalr/
- ImageSharp: https://docs.sixlabors.com/

### Frontend
- Angular: https://angular.dev/
- Ionic: https://ionicframework.com/docs
- Capacitor: https://capacitorjs.com/docs
- @angular/google-maps: https://github.com/angular/components
- Chart.js: https://www.chartjs.org/

### Data Sources
- GBIF Taxonomy: https://www.gbif.org/dataset/d7dddbf4-2cf0-4f39-9b2a-bb099caae36c
- IUCN Red List API: https://apiv3.iucnredlist.org/
- iNaturalist API: https://api.inaturalist.org/v1/docs/

### Geospatial
- PostGIS: https://postgis.net/documentation/
- Google Maps JS API: https://developers.google.com/maps/documentation/javascript
- NetTopologySuite: https://nettopologysuite.github.io/NetTopologySuite/

### Mobile
- Firebase Cloud Messaging: https://firebase.google.com/docs/cloud-messaging
- Capacitor Camera: https://capacitorjs.com/docs/apis/camera
- Capacitor Geolocation: https://capacitorjs.com/docs/apis/geolocation
