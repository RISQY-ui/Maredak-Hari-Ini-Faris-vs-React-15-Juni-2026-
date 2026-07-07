# 📚 Complete Backend → Frontend Guide

From Laravel to React.js - June 15-16, 2026

---

## 📊 Summary: From Backend to Frontend

### 1. Problems We Successfully Solved

| Aspect | Description |
|--------|-------------|
| **Root Cause** | When trying to create a React project using @latest, the error `SyntaxError: ... node:util ... styleText` appeared. This happened because the latest Vite installer (Vite 6) does not support Node.js version 18.19.1 installed on the laptop |
| **Genius Solution** | Downgraded the installer to Vite version 5 (`npm create vite@5`). Result: 100% compatible, safe, and smooth without changing Linux system configuration |

---

### 2. Successfully Executed Steps (Progress Checklist)

| No | Step | Status | Description |
|----|------|--------|-------------|
| 1 | Created React Folder | ✅ | Successfully created `frontend-faris` folder inside the Laravel practice directory |
| 2 | Installed Basic Dependencies | ✅ | `npm install` successfully downloaded all React.js basic packages |
| 3 | Tested Server | ✅ | `npm run dev` successfully displayed Vite + React template in Firefox browser |
| 4 | Installed Axios | ✅ | Shut down server (`Ctrl + C`) and installed Axios (`npm install axios`) as data fetcher from Laravel |

---

### 3. Position in Project Roadmap

| Stage | Status | Description |
|-------|--------|-------------|
| Stage 1 | ✅ | Initial setup |
| Stage 2 | ✅ | Frontend preparation |
| Stage 3 | ✅ | Axios installation |
| Stage 4 | ✅ | API Integration + CORS |

---

## 🚨 CORS Error & Solution (June 16, 2026)

### Issue Found

| Aspect | Description |
|--------|-------------|
| **Time** | 18:21 WIB |
| **Error Message** | `Cross-Origin Request Blocked: ... (Reason: CORS header 'Access-Control-Allow-Origin' missing). Status code: 200.` |
| **Root Cause** | Laravel by default only opens CORS for routes in `routes/api.php`. Since the `/model-name` route was placed in `routes/web.php`, Laravel detected Axios calls from React as a foreign threat and locked the gate |

---

### Solution

| Step | Command | Description |
|------|---------|-------------|
| 1 | Open `config/cors.php` | In VS Code Laravel |
| 2 | Change `'paths' => ['api/*', 'sanctum/csrf-cookie']` | To `'paths' => ['*']` |
| 3 | `Ctrl + S` | Save changes |

#### Final Result

| Status | Description |
|--------|-------------|
| ✅ | 100% Success! Firefox console completely clear of red errors |
| ✅ | Connection Established - React display successfully showed data from Laravel |

---

## 📖 Syntax Breakdown (Laravel)

### 1. Inside `NamaController.php` (Application Brain)

| Code | Meaning |
|------|---------|
| `namespace App\Http\Controllers;` | The address of this file within the project folder. So Laravel doesn't get lost when searching for it |
| `use App\Models\NamaModel;` | Command to call the Model file that holds the database. Without this, the Controller cannot touch the data table |
| `$data = NamaModel::all();` | Magic command to fetch ALL data rows in the database table |
| `return response()->json($data);` | Converts data into JSON format (preferred by React.js), then sends it to the browser |

---

### 2. Inside `routes/web.php` (URL Bridge)

| Code | Meaning |
|------|---------|
| `use App\Http\Controllers\NamaController;` | Introduces NamaController to the Laravel routing system |
| `Route::get('/model-name', [NamaController::class, 'index']);` | Creates a GET route. When someone opens `/model-name`, redirect to NamaController function `index()` |

---

### 3. Command to Create Dummy Data in Tinker

```php
App\Models\NamaModel::create([
    'model_name' => 'Faris First Project',
    'status' => true
]);
```

---

## 💻 Complete Code Guide

### 1. Terminal Commands

```bash
# 1. Create new Laravel project
composer create-project laravel/laravel project-name

# 2. Start Backend Laravel server
php artisan serve

# 3. Create Model & Migration together
php artisan make:model ModelName -m

# 4. Run migrations to database
php artisan migrate

# 5. Create API Controller
php artisan make:controller ModelController --api

# 6. Enter Tinker mode
php artisan tinker

# 7. Emergency commands (clear locked Linux queue)
sudo kill -9 9098
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo dpkg --configure -a

# 8. Go back one folder
cd ..

# 9. Install Node.js & NPM for React
sudo apt install nodejs npm
```

---

### 2. Code Inside Files

#### A. Database Table Structure File

**📍 Location:** `database/migrations/..._create_model_names_table.php`

```php
<?php

public function up(): void
{
    Schema::create('model_names', function (Blueprint $table) {
        $table->id();
        $table->string('model_name');
        $table->boolean('status')->default(true);
        $table->timestamps();
    });
}
```

---

#### B. Controller File

**📍 Location:** `app/Http/Controllers/ModelController.php`

```php
<?php

namespace App\Http\Controllers;

use App\Models\ModelName;
use Illuminate\Http\Request;

class ModelController extends Controller
{
    public function index()
    {
        $data = ModelName::all();
        return response()->json($data);
    }
}
```

---

#### C. Routing File

**📍 Location:** `routes/web.php`

```php
<?php

use App\Http\Controllers\ModelController;

Route::get('/model-name', [ModelController::class, 'index']);
```

---

#### D. CORS Configuration File

**📍 Location:** `config/cors.php`

```php
'paths' => ['*'],  // Changed from ['api/*', 'sanctum/csrf-cookie']
```

---

#### E. App.jsx (React)

**📍 Location:** `frontend-faris/src/App.jsx`

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [data, setData] = useState([]);

  useEffect(() => {
    axios.get('http://127.0.0.1:8000/model-name')
      .then(response => {
        setData(response.data);
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }, []);

  return (
    <div>
      <h1>Data from Laravel:</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>
            <strong>{item.model_name}</strong> - Status: {item.status ? 'Active' : 'Inactive'}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

---

## 🗺️ Complete Backend → Frontend Flow

### Flow 1: Manage Database (Database to Laravel)

| Step | Command | Description |
|------|---------|-------------|
| 1 | `php artisan make:model ModelName -m` | Create database table + Model |
| 2 | Edit migration file | Add `model_name` and `status` columns |
| 3 | `php artisan migrate` | Finalize table in database |
| 4 | `php artisan tinker` | Enter simulation mode |
| 5 | `ModelName::create([...])` | Insert sample data |

---

### Flow 2: Process Data (Laravel to API)

| Step | Command | Description |
|------|---------|-------------|
| 1 | `php artisan make:controller ModelController --api` | Create Controller |
| 2 | Edit `ModelController.php` | Fill `index()` with `ModelName::all()` and `response()->json()` |
| 3 | Edit `routes/web.php` | Add `Route::get('/model-name', [ModelController::class, 'index'])` |
| 4 | `php artisan serve` | Open shop window |
| 5 | Access `http://127.0.0.1:8000/model-name` | View JSON package in browser |

---

### Flow 3: Serve to Visitors (React.js)

| Step | Command | Description |
|------|---------|-------------|
| 1 | `sudo apt install nodejs npm` | Prepare React tools |
| 2 | `npm create vite@5` | Create React project folder |
| 3 | `npm install` | Install basic React packages |
| 4 | `npm install axios` | Install data fetcher |
| 5 | Edit `App.jsx` | Write code to fetch data from Laravel |
| 6 | `npm run dev` | Serve to visitors |

---

### Flow 4: Overcome CORS (Security Lock)

| Step | Command | Description |
|------|---------|-------------|
| 1 | Open `config/cors.php` | Laravel CORS configuration file |
| 2 | Change `'paths' => ['api/*', 'sanctum/csrf-cookie']` | To `'paths' => ['*']` |
| 3 | `Ctrl + S` | Save changes |
| 4 | Refresh browser | Data appears immediately! |

---

## 🎯 Core Flow (Simplest)

```
Create Data → Serve via Laravel → Open CORS → Fetch and Display with React.js
```

---

## ✅ Final Status Summary

| Component | Status |
|-----------|--------|
| Laravel Backend | ✅ |
| Endpoint `/model-name` | ✅ |
| CORS Configuration | ✅ |
| React + Vite 5 | ✅ |
| Axios | ✅ |
| Frontend Server | ✅ |
| API Integration | ✅ |
| Firefox Console | ✅ |

---

## 💡 Important Lessons

| Lesson | Description |
|--------|-------------|
| **Vite** | Vite 6 doesn't support Node.js 18.19.1 → use Vite 5 |
| **CORS** | Laravel only allows CORS for `api/*` routes by default |
| **CORS Solution** | Change `'paths' => ['api/*', 'sanctum/csrf-cookie']` to `'paths' => ['*']` |
| **Asterisk (*)** | Means allow all routes, suitable for local development |
| **Axios** | Data fetcher from backend to frontend |

---

**Last Updated:** June 16, 2026
