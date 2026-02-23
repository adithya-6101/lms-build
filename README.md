# 🎓 Modern Learning Management System (LMS)

<img width="2500" height="1357" alt="LMS Dashboard Banner" src="https://github.com/user-attachments/assets/e79e6a2f-9ddc-4c02-91c3-29a459f97adc" />

[![Next.js](https://img.shields.io/badge/Next.js-15-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Sanity](https://img.shields.io/badge/Sanity-Headless_CMS-orange?style=for-the-badge&logo=sanity)](https://www.sanity.io/)
[![Stripe](https://img.shields.io/badge/Stripe-Payments-635BFF?style=for-the-badge&logo=stripe)](https://stripe.com/)
[![Clerk](https://img.shields.io/badge/Clerk-Auth-6C47FF?style=for-the-badge&logo=clerk)](https://clerk.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=for-the-badge&logo=tailwind-css)](https://tailwindcss.com/)

## 🚀 Overview

The **Modern LMS Platform** is a scalable, full-stack education marketplace designed to bridge the gap between content creators and students. It features a robust **Next.js 15** frontend optimized for performance and SEO, coupled with a real-time **Sanity CMS** backend that allows for instant content propagation without rebuilds.

This platform handles the entire e-learning lifecycle: from course creation and rich-text lesson editing to secure student authentication, payment processing, and granular progress tracking.

## ✨ Key Features

### 👨‍🎓 Student Experience
* **Course Discovery:** Searchable and filterable course catalog with category-based browsing.
* **Seamless Checkout:** Integrated **Stripe Checkout** for secure, one-time course purchases.
* **Interactive Dashboard:** Real-time progress tracking (0-100%) as lessons are marked complete.
* **Multimedia Lessons:** Support for diverse content types including YouTube embeds, Loom videos, and rich text.

### 👨‍🏫 Instructor & Admin Power Tools
* **Sanity Studio Integration:** A fully customized CMS dashboard to manage Courses, Modules, Lessons, and Instructors.
* **Real-Time Preview:** "Presentation Mode" allows admins to edit content and see live previews on the production site before publishing.
* **Student Analytics:** View enrolled students, revenue generated, and individual completion statuses directly from the backend.

## 🏗️ Architectural Highlights

### 1. End-to-End Type Safety (Sanity TypeGen)
* **Problem:** Syncing TypeScript interfaces with a headless CMS schema is often manual and error-prone.
* **Solution:** I implemented **Sanity TypeGen** to automatically generate TypeScript definitions from my GROQ queries. This ensures that the frontend strictly adheres to the database schema, eliminating runtime errors caused by mismatched data shapes.

### 2. Resilient Payment Reconciliation (Stripe Webhooks)
* **Problem:** Relying on client-side redirects for payment confirmation is insecure and unreliable.
* **Solution:** I architected a robust webhook handler (`/api/webhook/stripe`) that verifies the Stripe signature on the server. It performs **asynchronous reconciliation**, unlocking course access in the database *only* after a cryptographic verification of the payment success event.

### 3. Real-Time Content Propagation (Sanity Live)
* **Problem:** Static sites often serve stale content until a rebuild is triggered.
* **Solution:** By utilizing **Sanity Live** and Next.js Server Actions, the platform achieves sub-second data propagation. When an instructor publishes a new lesson or fixes a typo, the change is reflected on the student's dashboard instantly via optimistic updates, without a page refresh.

## 🛠️ Tech Stack

* **Frontend:** Next.js 15 (App Router), React 19, Shadcn UI, Lucide React.
* **Backend / Content Lake:** Sanity.io (Structure Tool, Vision).
* **Authentication:** Clerk (Middleware protected routes).
* **Payments:** Stripe (Checkout Sessions & Webhooks).
* **Styling:** Tailwind CSS.

## 🚀 Getting Started

### Prerequisites
* Node.js (v18+)
* Stripe Account
* Sanity Account
* Clerk Account

### Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/modern-lms-platform.git](https://github.com/yourusername/modern-lms-platform.git)
    cd modern-lms-platform
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    # or
    pnpm install
    ```

3.  **Setup Environment Variables:**
    Create a `.env.local` file and add the following keys:

    ```env
    # Next.js
    NEXT_PUBLIC_BASE_URL=http://localhost:3000

    # Clerk Auth
    NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
    CLERK_SECRET_KEY=sk_test_...

    # Sanity CMS
    NEXT_PUBLIC_SANITY_PROJECT_ID=...
    NEXT_PUBLIC_SANITY_DATASET=production
    SANITY_API_TOKEN=...

    # Stripe Payments
    NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
    STRIPE_SECRET_KEY=sk_test_...
    STRIPE_WEBHOOK_SECRET=whsec_...
    ```

4.  **Run the Development Server:**
    ```bash
    npm run dev
    ```

5.  **Access the App:**
    * **LMS Frontend:** `http://localhost:3000`
    * **Admin Studio:** `http://localhost:3000/studio`

## 🧪 Stripe Webhook Setup

To process payments locally, you need to forward Stripe events to your local API route.

1.  **Listen to webhooks:**
    ```bash
    stripe listen --forward-to localhost:3000/api/stripe-checkout/webhook
    ```
    *(Note: For production, ensure the webhook endpoint is set to `https://your-domain.com/api/stripe-checkout/webhook`)*

## 📸 Screen Previews

### **Course Catalog & Student Dashboard**
<p float="left">
  <img src="https://github.com/user-attachments/assets/a71a1c19-9643-4c8f-9644-5e3e5a4e53c5" width="48%" />
  <img src="https://github.com/user-attachments/assets/a7b01831-5a3c-4702-8778-ec560b1b4420" width="48%" /> 
</p>

### **Admin Studio (CMS)**
Manage content and view enrollments directly from the Sanity Studio.
<img width="100%" alt="Sanity Admin Studio" src="https://github.com/user-attachments/assets/9034fc63-21cf-4046-81b8-4f602134af1e" />

### **Live Presentation Mode**
Admins can edit course content and preview changes live on the site without touching code.
<img width="100%" alt="Presentation Tool" src="https://github.com/user-attachments/assets/53ad0036-7600-42a2-96dc-faaa4917e163" />

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

**Built with ❤️ by [Adithya Cherukuri](https://www.linkedin.com/in/adithya-cherukuri-62005b199/)**
