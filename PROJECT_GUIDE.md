# Mad Commerce - Project Documentation

This guide provides a comprehensive overview of the **Mad Commerce** project, explaining its architecture, tech stack, and how the core components work together.

## 🚀 Tech Stack

- **Core**: [React](https://reactjs.org/) (Functional Components & Hooks)
- **Build Tool**: [Vite](https://vitejs.dev/) (Fast & Modern Development)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) (Utility-first CSS)
- **Routing**: [React Router Dom v6](https://reactrouter.com/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Animations**: [Framer Motion](https://www.framer.com/motion/)
- **Data Fetching**: [TanStack Query](https://tanstack.com/query/latest) (React Query)
- **Email Service**: [EmailJS](https://www.emailjs.com/) (Order confirmations & Contact form)
- **Database**: [Supabase](https://supabase.com/) (ChatBot message persistence)
- **Product API**: [Fakestore API](https://fakestoreapi.com/)

---

## 📂 Project Structure

```text
src/
├── components/          # Reusable UI components
│   ├── Layout.jsx      # Main wrapper with Navbar, Footer, and ChatBot
│   ├── Navbar.jsx      # Sticky navigation with Category dropdown
│   ├── ProductGrid.jsx # Fetches and filters products
│   ├── ChatBot.jsx     # AI assistant (Mocked)
│   └── ...
├── pages/               # Main page views
│   ├── Index.jsx       # Home page
│   ├── About.jsx       # Company info
│   ├── Contact.jsx     # Contact form and support
│   └── Login.jsx       # Login demonstration
├── lib/                 # Utility functions (e.g., cn for class merging)
├── App.jsx              # Routing and Provider setup
└── main.jsx             # React entry point
```

---

## 🛠️ Core Features & Components

### 1. Navigation & Routing (`App.jsx`, `Layout.jsx`)
The project uses **React Router** for seamless page transitions. Unlike traditional websites, it doesn't reload the entire page; only the content within the `<Outlet />` changes.
- **Layout System**: The `Layout` component wraps all routes, ensuring that the **Navbar**, **Footer**, and **ChatBot** are always visible to the user as they navigate.

### 2. Search Functionality (`Navbar.jsx`, `ProductGrid.jsx`)
- **Real-time Search**: Users can search for products by typing in the navbar search input (available on both desktop and mobile).
- **URL-based State**: Search queries are stored in URL parameters (`?search=...`) for shareable links and browser history.
- **Smart Filtering**: Products are filtered by title (case-insensitive) and can be combined with category filters.
- **Dynamic Headings**: The product grid heading updates to show search results context.

### 3. Product Grid & Filtering (`ProductGrid.jsx`)
- **Data Fetching**: Uses `useQuery` from TanStack Query to fetch product data from `fakestoreapi.com`. This provides efficient caching and loading states.
- **Category Filtering**: Uses **URL Search Parameters** (`?category=...`) for filtering by category.
- **Combined Filters**: Search and category filters work together seamlessly.

### 4. Email Notifications (`Checkout.jsx`, `Contact.jsx`)
- **Order Confirmations**: When a user places an order, an automated email is sent via EmailJS with order details (order ID, total amount, shipping address).
- **Contact Form**: The contact page sends messages directly to the business email using EmailJS.
- **Environment Variables**: Email service credentials are securely stored in `.env` file.

### 5. Smart ChatBot (`ChatBot.jsx`)
The ChatBot is an interactive support assistant providing real-time help.
- **Supabase Integration**: Chat messages are persisted to a Supabase database.
- **Message Isolation & Privacy**: 
    - **Strict Filtering**: Messages are strictly filtered by either a `user_id` (for logged-in users) or a unique `session_id` (for guests persisted in `localStorage`).
    - **Privacy Guard**: The system prevents fetching or saving messages if no valid identity is present, ensuring that chat histories are isolated and private to each user/device.
- **Mock Logic**: Uses a local logic engine for instant, relevant replies to common queries.
- **Regex Detection**: Scans user input for keywords (like "shipping", "price", "hello") to trigger contextual help.
- **UI/UX**: Features smooth animations using `framer-motion`, auto-scrolling, and a responsive floating design.

### 6. Newsletter Subscription (`Footer.jsx`)
- **Interactive UI**: Users can subscribe to updates directly from the footer.
- **Micro-interactions**: Provides instant UI feedback and validation upon subscription.
- **Modern Design**: Seamlessly integrated into the dark-themed footer with glassmorphic input fields.

### 7. Authentication System (`AuthContext.jsx`)
The project features a hybrid authentication system to demonstrate both local and API-based user management.
- **Context API**: Uses React Context to provide a global `user` state across the entire application.
- **Persistence**: Logged-in user data is persisted in `localStorage`, satisfying the requirement for the user to stay logged in after page refreshes.
- **Hybrid Source**:
    - **API Users**: Validates credentials against the **Fakestore API** for pre-existing mock users.
    - **Local Persistence**: New accounts created via the Signup page are stored in `local_users` within `localStorage`, allowing them to "persist" even though there is no real backend database for new users.

### 8. Custom Styling & Aesthetics
The visual identity is built on a custom, premium design system.
- **Tailwind Framework**: Uses Tailwind CSS for all layout and styling, ensuring consistency and performance.
- **Design Tokens**: Custom colors (like `navbar`, `background`, `primary`) are defined in `tailwind.config.js` and mapped to CSS variables for dynamic theme support.
- **Mobile-First**: Every component is fully responsive, utilizing Tailwind's breakpoint prefixes (`md:`, `lg:`) for a seamless experience on all devices.
- **Micro-animations**: Enhanced with `framer-motion` for subtle hover effects, page transitions, and interactive feedback.

---

## 📄 Page Breakdown

- **Home (`/`)**: Shows the Hero Banner, search functionality, and the filtered/all products list.
- **Product Detail (`/product/:id`)**: Displays detailed product information with add-to-cart functionality.
- **Checkout (`/checkout`)**: Complete checkout flow with shipping form and order confirmation email.
- **Contact (`/contact`)**: Premium support page with contact cards and EmailJS-powered contact form.
- **About (`/about`)**: Storytelling page highlighting the brand's values and mission.
- **Login (`/login`)**: Modern authentication UI demonstration with Supabase integration.

---

## ⚡ Development Workflow

1. **Start Dev Server**: `npm run dev`
2. **Build for Production**: `npm run build`
3. **Preview Build**: `npm run preview`

The project is designed to be **lightweight, fast, and easy to maintain**, focusing on a premium user experience with minimal external dependencies.
