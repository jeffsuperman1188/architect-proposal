mkdir archproposal && cd archproposal

npm create vite@latest . -- --template react
npm install

# Core dependencies
npm install @supabase/supabase-js @supabase/auth-helpers-react
npm install @stripe/stripe-js
npm install react-router-dom
npm install react-hook-form zod @hookform/resolvers
npm install react-to-print
npm install sonner
npm install lucide-react
npm install clsx

# Dev dependencies
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
// package.json
{
  "name": "archproposal",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@hookform/resolvers": "^3.3.4",
    "@supabase/auth-helpers-react": "^0.5.0",
    "@supabase/supabase-js": "^2.39.0",
    "@stripe/stripe-js": "^3.0.0",
    "clsx": "^2.1.0",
    "lucide-react": "^0.344.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-hook-form": "^7.51.0",
    "react-router-dom": "^6.22.0",
    "react-to-print": "^2.15.1",
    "sonner": "^1.4.0",
    "zod": "^3.22.4"
  },
  "devDependencies": {
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "@vitejs/plugin-react": "^4.2.0",
    "autoprefixer": "^10.4.18",
    "postcss": "^8.4.35",
    "tailwindcss": "^3.4.1",
    // vite.config.js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
  build: {
    outDir: 'dist',
    sourcemap: false,
  },
})
// vercel.json
{
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": "vite",
  "rewrites": [
    { "source": "/api/(.*)", "destination": "/api/$1" },
    { "source": "/(.*)", "destination": "/index.html" }
  ],
  "headers": [
    {
      "source": "/api/(.*)",
      "headers": [
        { "key": "Access-Control-Allow-Origin", "value": "*" },
        { "key": "Access-Control-Allow-Methods", "value": "GET,POST,OPTIONS" },
        { "key": "Access-Control-Allow-Headers", "value": "Content-Type,Authorization" }
      ]
    },
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Frame-Options", "value": "DENY" },
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" },
        { "key": "Strict-Transport-Security", "value": "max-age=31536000; includeSubDomains" }
      ]
    }
  ]
}
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./index.html', './src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        heading: ['Inter', 'system-ui', 'sans-serif'],
      },
      colors: {
        brand: {
          50:  '#f0f4ff',
          100: '#e0e9ff',
          500: '#3b5bdb',
          600: '#2f4ac7',
          700: '#2541b2',
          900: '#1a2d7a',
        },
      },
    },
  },
  plugins: [],
}
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <!-- Primary SEO -->
    <title>ArchProposal — AI Proposal Writer for Freelance Architects</title>
    <meta name="description" content="Generate polished, client-winning architectural proposals in under 2 minutes. Tailored to every project, branded to your firm." />
    <meta name="keywords" content="architectural proposal template, freelance architect tools, project proposal writer, architect business tools, AIA proposal" />
    <link rel="canonical" href="https://archproposal.com" />

    <!-- Open Graph -->
    <meta property="og:title" content="ArchProposal — Win More Projects" />
    <meta property="og:description" content="AI-written proposals tailored to every client." />
    <meta property="og:image" content="https://archproposal.com/og-image.png" />
    <meta property="og:url" content="https://archproposal.com" />
    <meta property="og:type" content="website" />

    <!-- Twitter -->
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content="ArchProposal — AI Proposal Writer" />
    <meta name="twitter:description" content="Stop spending 5 hours on proposals." />

    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />

    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
// src/styles/tokens.js
export const tokens = {
  colors: {
    brand:    '#3b5bdb',
    brandDark:'#2541b2',
    dark:     '#111827',
    gray:     '#6b7280',
    grayLight:'#f3f4f6',
    border:   '#e5e7eb',
    white:    '#ffffff',
    success:  '#10b981',
    warning:  '#f59e0b',
    danger:   '#ef4444',
  },
  fonts: {
    sans:    "'Inter', system-ui, sans-serif",
    heading: "'Inter', system-ui, sans-serif",
  },
  spacing: {
    xs: '4px',
    sm: '8px',
    md: '16px',
    lg: '24px',
    xl: '32px',
    '2xl': '48px',
    '3xl': '64px',
  },
  radius: {
    sm: '6px',
    md: '10px',
    lg: '16px',
    full: '9999px',
  },
  shadow: {
    sm: '0 1px 3px rgba(0,0,0,0.08)',
    md: '0 4px 16px rgba(0,0,0,0.08)',
    lg: '0 8px 32px rgba(0,0,0,0.10)',
  },
}

export const PLAN_LIMITS = {
  free:   { proposals: 3, pdf: true, branding: false, history: false, seats: 1 },
  pro:    { proposals: -1, pdf: true, branding: true, history: true, seats: 1 },
  agency: { proposals: -1, pdf: true, branding: true, history: true, seats: 5 },
}
/* src/styles/global.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Inter', system-ui, sans-serif;
    background: #f9fafb;
    color: #111827;
    -webkit-font-smoothing: antialiased;
  }

  h1, h2, h3, h4 {
    font-family: 'Inter', system-ui, sans-serif;
    font-weight: 700;
    letter-spacing: -0.02em;
  }
}

@layer components {
  .btn {
    @apply inline-flex items-center justify-center gap-2 px-5 py-2.5 rounded-lg font-semibold text-sm transition-all duration-150 cursor-pointer border-0 outline-none;
  }

  .btn-primary {
    @apply btn bg-brand-600 text-white hover:bg-brand-700 shadow-sm;
  }

  .btn-secondary {
    @apply btn bg-white text-gray-700 border border-gray-200 hover:bg-gray-50;
  }

  .btn-danger {
    @apply btn bg-red-500 text-white hover:bg-red-600;
  }

  .btn-lg {
    @apply px-7 py-3.5 text-base rounded-xl;
  }

  .input {
    @apply w-full px-4 py-2.5 rounded-lg border border-gray-200 text-sm
           bg-white text-gray-900 placeholder-gray-400
           focus:outline-none focus:ring-2 focus:ring-brand-500/30 focus:border-brand-500
           transition-colors duration-150;
  }

  .label {
    @apply block text-sm font-semibold text-gray-700 mb-1.5;
  }

  .card {
    @apply bg-white rounded-xl border border-gray-200 shadow-sm;
  }

  .error-msg {
    @apply text-red-500 text-xs mt-1 flex items-center gap-1;
  }

  .badge {
    @apply inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold;
  }

  .badge-green  { @apply badge bg-emerald-100 text-emerald-700; }
  .badge-blue   { @apply badge bg-blue-100 text-blue-700; }
  .badge-yellow { @apply badge bg-yellow-100 text-yellow-700; }
  .badge-gray   { @apply badge bg-gray-100 text-gray-600; }
  .badge-red    { @apply badge bg-red-100 text-red-600; }
}

/* ─── Print styles ──────────────────────────────── */
@media print {
  body { background: white !important; }
  .no-print { display: none !important; }
  .print-only { display: block !important; }

  .pdf-page {
    page-break-after: always;
    break-after: page;
  }

  * {
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
  }
}
// src/lib/supabase.js
import { createClient } from '@supabase/supabase-js'

const supabaseUrl  = import.meta.env.VITE_SUPABASE_URL
const supabaseKey  = import.meta.env.VITE_SUPABASE_ANON_KEY

if (!supabaseUrl || !supabaseKey) {
  throw new Error('Missing Supabase environment variables')
}

export const supabase = createClient(supabaseUrl, supabaseKey, {
  auth: {
    persistSession: true,
    autoRefreshToken: true,
    detectSessionInUrl: true,
  },
})

// ── Auth helpers ─────────────────────────────────

export async function signUp({ email, password, name, firmName }) {
  const { data, error } = await supabase.auth.signUp({
    email,
    password,
    options: {
      data: { name, firm_name: firmName },
    },
  })
  if (error) throw error

  // Create profile row
  if (data.user) {
    const { error: profileError } = await supabase
      .from('profiles')
      .insert({
        id:        data.user.id,
        email,
        name,
        firm_name: firmName,
        plan:      'free',
      })
    if (profileError) throw profileError
  }

  return data
}

export async function signIn({ email, password }) {
  const { data, error } = await supabase.auth.signInWithPassword({
    email,
    password,
  })
  if (error) throw error
  return data
}

export async function signOut() {
  const { error } = await supabase.auth.signOut()
  if (error) throw error
}

export async function getProfile(userId) {
  const { data, error } = await supabase
    .from('profiles')
    .select('*')
    .eq('id', userId)
    .single()
  if (error) throw error
  return data
}

export async function updateProfile(userId, updates) {
  const { data, error } = await supabase
    .from('profiles')
    .update(updates)
    .eq('id', userId)
    .select()
    .single()
  if (error) throw error
  return data
}

// ── Proposals helpers ─────────────────────────────

export async function saveProposal(proposalData) {
  const { data, error } = await supabase
    .from('proposals')
    .insert(proposalData)
    .select()
    .single()
  if (error) throw error
  return data
}

export async function getProposals(userId) {
  const { data, error } = await supabase
    .from('proposals')
    .select('*')
    .eq('user_id', userId)
    .order('created_at', { ascending: false })
  if (error) throw error
  return data ?? []
}

export async function getProposal(id) {
  const { data, error } = await supabase
    .from('proposals')
    .select('*')
    .eq('id', id)
    .single()
  if (error) throw error
  return data
}

export async function updateProposalStatus(id, status) {
  const { error } = await supabase
    .from('proposals')
    .update({ status })
    .eq('id', id)
  if (error) throw error
}

export async function deleteProposal(id) {
  const { error } = await supabase
    .from('proposals')
    .delete()
    .eq('id', id)
  if (error) throw error
    "vite": "^5.1.0"
  }
}
