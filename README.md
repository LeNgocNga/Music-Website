# 🎵 Music Streaming Website

---

## 📖 Overview

An online music streaming website built with **ASP.NET MVC Framework** and **C#**, designed to replace traditional music consumption methods with a modern, centralized platform. The system allows users to search, stream, and organize music into personal playlists, while providing administrators with full content management capabilities.

---

## ✨ Key Features

### 👤 User Features
- Register and login with email and password
- Search for songs by title or artist
- Stream music directly in the browser with continuous auto-play
- Add songs to personal favorites list
- Create and manage personal playlists
- Add or remove songs from playlists

### 🛠️ Admin / Manager Features
- Manage songs — add, edit, delete, view details
- Manage artists — add, edit, delete
- Manage genres — add, edit, delete
- Manage themes — add, edit, delete, assign songs
- Manage user accounts — add, edit, delete

---

## 🛠️ Tech Stack

| Technology | Description |
|------------|-------------|
| **C#** | Primary programming language |
| **ASP.NET MVC Framework** | Web application architecture (Model–View–Controller) |
| **.NET Framework** | Runtime and application development platform |
| **SQL Server** | Relational database management |
| **LINQ** | Data querying integrated directly in C# |
| **HTML5** | Page structure and audio support |
| **CSS3** | Styling and responsive layout |
| **Bootstrap** | UI component library and responsive grid |
| **JavaScript** | Client-side interactivity and dynamic content |
| **jQuery** | DOM manipulation and AJAX requests |
| **Git / GitHub** | Source control and version management |
| **Visual Studio 2022** | IDE for development and debugging |

---

## 🏗️ Architecture

The project follows the **MVC (Model–View–Controller)** pattern:

| Layer | Responsibility |
|-------|---------------|
| **Model** | Business data, entities, and application logic |
| **View** | HTML templates rendered with data from the Controller |
| **Controller** | Handles HTTP requests, communicates with Model, returns Views or JSON |

**Request flow:**
```
Client → Controller → (Model ↔ Database) → View → Controller → Client
```
For data-only requests (AJAX), the Controller returns JSON directly without rendering a View.

---

## 🗂️ Database Schema

| Table | Key Columns | Purpose |
|-------|-------------|---------|
| `Nhac` | MaBH, TenBH, Files, image, NgayPH, MaCS, MaTL, MaCD | Song records with file path, image, and foreign keys |
| `account` | MaTK, Email, PassWord, Role, Ten | User accounts and role management |
| `Playlist` | stt, MaTK, MaBH, TenPL | Personal playlist entries |
| `TheLoai` | MaTL, TenTL | Music genres |
| `CaSi` | MaCS, TenCS | Artist profiles |
| `ChuDe` | MaCD, TenCD, Picture, Color | Themed collections with cover image and color |

**Relationships:**
- `Nhac` references `CaSi`, `TheLoai`, and `ChuDe` via foreign keys
- `Playlist` links `account` to `Nhac`
- `account.Role` determines user vs. admin access (Role = 1 for admin, 0 for user)

---

## 👤 Role-Based Access

| Role | Access |
|------|--------|
| **Admin (Role = 1)** | Full CRUD for songs, artists, genres, themes, and user accounts |
| **User (Role = 0)** | Search, stream, manage personal playlists and favorites |

New registrations are always assigned **User** role by default.

---

## 🚀 Getting Started

### Prerequisites
- [Visual Studio 2022](https://visualstudio.microsoft.com/) (Community edition or higher)
- [.NET Framework](https://dotnet.microsoft.com/en-us/download/dotnet-framework) >= 4.x
- [SQL Server](https://www.microsoft.com/en-us/sql-server) 2019 or later
- [SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) 20
- Git

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd music-streaming-website
```

### Database Setup

```sql
-- 1. Create the database
CREATE DATABASE MusicDB;

-- 2. Run the SQL scripts from /database folder in order:
--    - schema.sql  (create tables)
--    - seed.sql    (optional: insert sample data)
```

### Configure Connection String

In `Web.config`, update the connection string:

```xml
<connectionStrings>
  <add name="MusicDBContext"
       connectionString="Data Source=YOUR_SERVER;Initial Catalog=MusicDB;Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```

### Run the Application

1. Open `MusicWebsite.sln` in Visual Studio 2022
2. Build the solution (`Ctrl + Shift + B`)
3. Press `F5` to run (or `Ctrl + F5` to run without debug)
4. The browser will open at `https://localhost:{port}`

---

## 📁 Project Structure

```
MusicWebsite/
├── Controllers/              # MVC Controllers (request handling)
│   ├── AccountController.cs
│   ├── HomeController.cs
│   ├── SongController.cs
│   ├── PlaylistController.cs
│   └── AdminController.cs
├── Models/                   # Entity models and ViewModels
│   ├── Nhac.cs
│   ├── Account.cs
│   ├── Playlist.cs
│   ├── CaSi.cs
│   ├── TheLoai.cs
│   └── ChuDe.cs
├── Views/                    # Razor View templates (.cshtml)
│   ├── Home/
│   ├── Account/
│   ├── Song/
│   ├── Playlist/
│   ├── Admin/
│   └── Shared/               # Layout (_Layout.cshtml), partials
├── Content/                  # CSS stylesheets
├── Scripts/                  # JavaScript and jQuery files
├── App_Data/                 # Local database files (if any)
├── Web.config                # App configuration
└── MusicWebsite.sln          # Visual Studio solution file
```

---

## 📷 UI Screens

| Screen | Description |
|--------|-------------|
| **Login** | Two-column layout with brand panel and login form |
| **Register** | Same layout with email, password, and display name fields |
| **Home / Dashboard** | Songs grouped by theme with album art cards |
| **Search** | Keyword search with live results display |
| **User Sidebar** | Home, Search, Library, Create Playlist, Favorites |
| **Admin Sidebar** | Extended with Song Management and Account Management |
| **Song Management** | Table with song title, image, release date, artist, edit/detail actions |
| **Artist Management** | Table with artist code, name, edit/delete actions |
| **Genre Management** | Table with genre code, name, edit/delete actions |
| **Theme Management** | Table with theme code, name, cover image, color, edit/delete |
| **Account Management** | Table with email, password, role, name, edit/delete |
| **Playlist View** | Named playlist with song list, genre, and release date |
| **Song Detail** | Song title, artist, date, related songs from same artist |
| **Favorites** | Heart-icon playlist showing all liked songs |
| **Create Playlist** | Name input with song selector and checkbox list |

---

## 📈 Strengths

- ✅ Clean MVC separation — easy to maintain and extend
- ✅ Role-based access control (admin vs. user)
- ✅ Continuous music playback across page navigation
- ✅ Personal playlist and favorites management
- ✅ Responsive layout compatible with desktop browsers
- ✅ Source code versioned and backed up via GitHub

---

## ⚠️ Known Limitations

- Page load speed may be inconsistent under high traffic
- No offline playback support
- No social sharing or community features
- Advanced search (by year, genre filter) not yet implemented
- Mobile and cross-platform compatibility not fully optimized

---

## 🔭 Future Development

- 🤖 **AI Recommendation Engine** — suggest songs based on listening history
- 📱 **Mobile Optimization** — full responsive support for phones and tablets
- 🎙️ **Podcast Support** — extend content beyond music
- 🌐 **Internationalization** — multi-language and international music catalog
- 🔗 **Social Features** — share playlists, follow artists, community events
- 📊 **Analytics Dashboard** — track plays, trending songs, user activity
- 🔒 **Offline Mode** — allow premium users to download songs

---

## 📚 References

- Adam Freeman — *Pro ASP.NET Core 7* (Manning Publications, 2023)
- Paul Deitel, Harvey Deitel — *Visual C# How to Program*
- [ASP.NET MVC Documentation](https://docs.microsoft.com/en-us/aspnet/mvc/)
- [SQL Server Documentation](https://docs.microsoft.com/en-us/sql/sql-server/)
- [Bootstrap Documentation](https://getbootstrap.com/docs/)
- [jQuery Documentation](https://api.jquery.com/)

---

<div align="center">
  <sub>Academic Project · University of Information Technology (UIT) · Faculty of Software Engineering · .NET Technology · 2024</sub>
</div>
