# Smart Bookmark App

A simple bookmark manager built with Next.js, Supabase, and Tailwind CSS.

## Features

- ✅ Google OAuth authentication (no email/password)
- ✅ Add bookmarks with title and URL
- ✅ Private bookmarks (each user sees only their own)
- ✅ Real-time updates across multiple tabs
- ✅ Delete bookmarks
- ✅ Responsive design with Tailwind CSS

## Tech Stack

- **Frontend**: Next.js (App Router), TypeScript, Tailwind CSS
- **Backend**: Supabase (Auth, Database, Realtime)
- **Deployment**: Vercel

## Setup Instructions

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd smart-bookmark-app
```

### 2. Install dependencies
```bash
npm install
```

### 3. Set up Supabase

1. Create a new Supabase project at [supabase.com](https://supabase.com)
2. Go to Authentication > Settings and enable Google OAuth
3. Add your Google OAuth credentials
4. Run the SQL schema from `supabase-schema.sql` in the Supabase SQL editor

### 4. Environment variables

Create a `.env.local` file in the root directory:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Get these values from your Supabase project settings.

### 5. Run the development server
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Database Schema

The app uses a `bookmarks` table with the following structure:

```sql
CREATE TABLE bookmarks (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  title TEXT NOT NULL,
  url TEXT NOT NULL,
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

Row Level Security (RLS) is enabled to ensure users can only access their own bookmarks.

## Deployment

The app is ready to be deployed on Vercel:

1. Push your code to GitHub
2. Connect your GitHub repository to Vercel
3. Add the environment variables in Vercel dashboard
4. Deploy!

## Usage

1. Click "Login with Google" to authenticate
2. Add bookmarks using the title and URL fields
3. Your bookmarks are saved and synced in real-time
4. Open multiple tabs to see real-time updates
5. Click "Delete" to remove bookmarks
6. Click "Logout" to sign out

## Security Features

- Row Level Security (RLS) ensures data privacy
- Users can only access their own bookmarks
- Secure Google OAuth integration
- Environment variables for sensitive data
