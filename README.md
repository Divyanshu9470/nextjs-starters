# nextjs-starters
├── .github
    └── workflows
    │   └── nextjs.yml
├── .gitignore
├── LICENSE
├── README.md
├── app
    ├── favicon.ico
    ├── globals.css
    ├── layout.tsx
    └── not-found.tsx
├── components.json
├── components
    ├── common
    │   └── Navbar.tsx
    └── ui
    │   └── button.tsx
├── context
    └── userContext.js
├── lib
    └── utils.ts
├── next.config.ts
├── package-lock.json
├── package.json
├── pages
    ├── _app.tsx
    └── index.tsx
├── postcss.config.mjs
├── public
    ├── file.svg
    ├── globe.svg
    ├── next.svg
    ├── vercel.svg
    └── window.svg
└── tsconfig.json


/.github/workflows/nextjs.yml:
--------------------------------------------------------------------------------
 1 | # Sample workflow for building and deploying a Next.js site to GitHub Pages
 2 | #
 3 | # To get started with Next.js see: https://nextjs.org/docs/getting-started
 4 | #
 5 | name: Deploy Next.js site to Pages
 6 | 
 7 | on:
 8 |   # Runs on pushes targeting the default branch
 9 |   push:
10 |     branches: ["main"]
11 | 
12 |   # Allows you to run this workflow manually from the Actions tab
13 |   workflow_dispatch:
14 | 
15 | # Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
16 | permissions:
17 |   contents: read
18 |   pages: write
19 |   id-token: write
20 | 
21 | # Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
22 | # However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
23 | concurrency:
24 |   group: "pages"
25 |   cancel-in-progress: false
26 | 
27 | jobs:
28 |   # Build job
29 |   build:
30 |     runs-on: ubuntu-latest
31 |     steps:
32 |       - name: Checkout
33 |         uses: actions/checkout@v4
34 |       - name: Detect package manager
35 |         id: detect-package-manager
36 |         run: |
37 |           if [ -f "${{ github.workspace }}/yarn.lock" ]; then
38 |             echo "manager=yarn" >> $GITHUB_OUTPUT
39 |             echo "command=install" >> $GITHUB_OUTPUT
40 |             echo "runner=yarn" >> $GITHUB_OUTPUT
41 |             exit 0
42 |           elif [ -f "${{ github.workspace }}/package.json" ]; then
43 |             echo "manager=npm" >> $GITHUB_OUTPUT
44 |             echo "command=ci" >> $GITHUB_OUTPUT
45 |             echo "runner=npx --no-install" >> $GITHUB_OUTPUT
46 |             exit 0
47 |           else
48 |             echo "Unable to determine package manager"
49 |             exit 1
50 |           fi
51 |       - name: Setup Node
52 |         uses: actions/setup-node@v4
53 |         with:
54 |           node-version: "20"
55 |           cache: ${{ steps.detect-package-manager.outputs.manager }}
56 |       - name: Setup Pages
57 |         uses: actions/configure-pages@v5
58 |         with:
59 |           # Automatically inject basePath in your Next.js configuration file and disable
60 |           # server side image optimization (https://nextjs.org/docs/api-reference/next/image#unoptimized).
61 |           #
62 |           # You may remove this line if you want to manage the configuration yourself.
63 |           static_site_generator: next
64 |       - name: Restore cache
65 |         uses: actions/cache@v4
66 |         with:
67 |           path: |
68 |             .next/cache
69 |           # Generate a new cache whenever packages or source files change.
70 |           key: ${{ runner.os }}-nextjs-${{ hashFiles('**/package-lock.json', '**/yarn.lock') }}-${{ hashFiles('**.[jt]s', '**.[jt]sx') }}
71 |           # If source files changed but packages didn't, rebuild from a prior cache.
72 |           restore-keys: |
73 |             ${{ runner.os }}-nextjs-${{ hashFiles('**/package-lock.json', '**/yarn.lock') }}-
74 |       - name: Install dependencies
75 |         run: ${{ steps.detect-package-manager.outputs.manager }} ${{ steps.detect-package-manager.outputs.command }}
76 |       - name: Build with Next.js
77 |         run: ${{ steps.detect-package-manager.outputs.runner }} next build
78 |       - name: Upload artifact
79 |         uses: actions/upload-pages-artifact@v3
80 |         with:
81 |           path: ./out
82 | 
83 |   # Deployment job
84 |   deploy:
85 |     environment:
86 |       name: github-pages
87 |       url: ${{ steps.deployment.outputs.page_url }}
88 |     runs-on: ubuntu-latest
89 |     needs: build
90 |     steps:
91 |       - name: Deploy to GitHub Pages
92 |         id: deployment
93 |         uses: actions/deploy-pages@v4
94 | 


--------------------------------------------------------------------------------
/.gitignore:
--------------------------------------------------------------------------------
 1 | # See https://help.github.com/articles/ignoring-files/ for more about ignoring files.
 2 | 
 3 | # dependencies
 4 | /node_modules
 5 | /.pnp
 6 | .pnp.*
 7 | .yarn/*
 8 | !.yarn/patches
 9 | !.yarn/plugins
10 | !.yarn/releases
11 | !.yarn/versions
12 | 
13 | # testing
14 | /coverage
15 | 
16 | # next.js
17 | /.next/
18 | /out/
19 | 
20 | # production
21 | /build
22 | 
23 | # misc
24 | .DS_Store
25 | *.pem
26 | 
27 | # debug
28 | npm-debug.log*
29 | yarn-debug.log*
30 | yarn-error.log*
31 | .pnpm-debug.log*
32 | 
33 | # env files (can opt-in for committing if needed)
34 | .env*
35 | 
36 | # vercel
37 | .vercel
38 | 
39 | # typescript
40 | *.tsbuildinfo
41 | next-env.d.ts
42 | 


--------------------------------------------------------------------------------
/LICENSE:
--------------------------------------------------------------------------------
 1 | MIT License
 2 | 
 3 | Copyright (c) 2025 The Bipu
 4 | 
 5 | Permission is hereby granted, free of charge, to any person obtaining a copy
 6 | of this software and associated documentation files (the "Software"), to deal
 7 | in the Software without restriction, including without limitation the rights
 8 | to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
 9 | copies of the Software, and to permit persons to whom the Software is
10 | furnished to do so, subject to the following conditions:
11 | 
12 | The above copyright notice and this permission notice shall be included in all
13 | copies or substantial portions of the Software.
14 | 
15 | THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
16 | IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
17 | FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
18 | AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
19 | LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
20 | OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
21 | SOFTWARE.
22 | 


--------------------------------------------------------------------------------
/README.md:
--------------------------------------------------------------------------------
 1 | # 🚀 Next.js Starters
 2 | 
 3 | A **minimal and scalable starter template** for building modern web apps with **Next.js (App Router)**. This repo gives you a clean foundation to kickstart your projects without extra setup overhead.
 4 | 
 5 | ## 📂 Project Structure
 6 | 
 7 | ```
 8 | .
 9 | ├── app/            # Next.js App Router pages
10 | │   └── page.tsx    # Home page
11 | ├── components/     # Reusable UI components
12 | ├── context/        # React context providers
13 | ├── lib/            # Utility functions, helpers
14 | ├── pages/          # (Optional) Legacy Pages Router
15 | ├── public/         # Static assets (images, icons, etc.)
16 | ├── styles/         # Global styles
17 | ├── next.config.ts  # Next.js configuration
18 | ├── tsconfig.json   # TypeScript configuration
19 | └── package.json
20 | ```
21 | 
22 | ## ⚡ Features
23 | 
24 | * ✅ **Next.js App Router** setup (`app/` directory)
25 | * ✅ **TypeScript** enabled by default
26 | * ✅ **Font optimization** with `next/font` (Geist font)
27 | * ✅ Clean folder structure for scaling projects
28 | * ✅ Ready-to-use configuration files (`tsconfig`, `next.config`, etc.)
29 | 
30 | ## 🚀 Getting Started
31 | 
32 | Clone the repo:
33 | 
34 | ```bash
35 | git clone https://github.com/the-bipu/nextjs-starters.git
36 | cd nextjs-starters
37 | ```
38 | 
39 | Install dependencies:
40 | 
41 | ```bash
42 | npm install
43 | # or
44 | yarn install
45 | # or
46 | pnpm install
47 | ```
48 | 
49 | Run the development server:
50 | 
51 | ```bash
52 | npm run dev
53 | ```
54 | 
55 | Open [http://localhost:3000](http://localhost:3000) with your browser to see your app.
56 | 
57 | ## 🛠️ Scripts
58 | 
59 | | Command | Action |
60 | |---------|--------|
61 | | `npm run dev` | Start dev server (http://localhost:3000) |
62 | | `npm run build` | Build production version |
63 | | `npm run start` | Run production server |
64 | | `npm run lint` | Run ESLint checks |
65 | 
66 | ## 📦 Deployment
67 | 
68 | You can deploy this template easily to platforms like:
69 | 
70 | * **Vercel** (recommended)
71 | * **Netlify** 
72 | * **Dockerized servers**
73 | 
74 | ### For Vercel:
75 | 1. Push your repo to GitHub
76 | 2. Import into Vercel dashboard
77 | 3. Done 🎉
78 | 
79 | ## 📌 Roadmap
80 | 
81 | * Add Tailwind CSS + shadcn/ui integration (optional branch)
82 | * Example API routes setup
83 | * Authentication template (NextAuth.js)
84 | * CI/CD workflow with GitHub Actions
85 | 
86 | ## 🤝 Contributing
87 | 
88 | Contributions, issues, and feature requests are welcome! Feel free to check issues or submit a PR.
89 | 
90 | ## 📜 License
91 | 
92 | This project is licensed under the MIT License.
93 | 
94 | ---
95 | 
96 | 🔥 **Ready to build?** Fork this repo and start your Next.js project today!
97 | 


--------------------------------------------------------------------------------
/app/favicon.ico:
--------------------------------------------------------------------------------
https://raw.githubusercontent.com/the-bipu/nextjs-starters/main/app/favicon.ico


--------------------------------------------------------------------------------
/app/globals.css:
--------------------------------------------------------------------------------
  1 | @import "tailwindcss";
  2 | @import "tw-animate-css";
  3 | 
  4 | @custom-variant dark (&:is(.dark *));
  5 | 
  6 | @theme inline {
  7 |   --color-background: var(--background);
  8 |   --color-foreground: var(--foreground);
  9 |   --font-sans: var(--font-geist-sans);
 10 |   --font-mono: var(--font-geist-mono);
 11 |   --color-sidebar-ring: var(--sidebar-ring);
 12 |   --color-sidebar-border: var(--sidebar-border);
 13 |   --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
 14 |   --color-sidebar-accent: var(--sidebar-accent);
 15 |   --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
 16 |   --color-sidebar-primary: var(--sidebar-primary);
 17 |   --color-sidebar-foreground: var(--sidebar-foreground);
 18 |   --color-sidebar: var(--sidebar);
 19 |   --color-chart-5: var(--chart-5);
 20 |   --color-chart-4: var(--chart-4);
 21 |   --color-chart-3: var(--chart-3);
 22 |   --color-chart-2: var(--chart-2);
 23 |   --color-chart-1: var(--chart-1);
 24 |   --color-ring: var(--ring);
 25 |   --color-input: var(--input);
 26 |   --color-border: var(--border);
 27 |   --color-destructive: var(--destructive);
 28 |   --color-accent-foreground: var(--accent-foreground);
 29 |   --color-accent: var(--accent);
 30 |   --color-muted-foreground: var(--muted-foreground);
 31 |   --color-muted: var(--muted);
 32 |   --color-secondary-foreground: var(--secondary-foreground);
 33 |   --color-secondary: var(--secondary);
 34 |   --color-primary-foreground: var(--primary-foreground);
 35 |   --color-primary: var(--primary);
 36 |   --color-popover-foreground: var(--popover-foreground);
 37 |   --color-popover: var(--popover);
 38 |   --color-card-foreground: var(--card-foreground);
 39 |   --color-card: var(--card);
 40 |   --radius-sm: calc(var(--radius) - 4px);
 41 |   --radius-md: calc(var(--radius) - 2px);
 42 |   --radius-lg: var(--radius);
 43 |   --radius-xl: calc(var(--radius) + 4px);
 44 | }
 45 | 
 46 | :root {
 47 |   --radius: 0.625rem;
 48 |   --background: oklch(1 0 0);
 49 |   --foreground: oklch(0.145 0 0);
 50 |   --card: oklch(1 0 0);
 51 |   --card-foreground: oklch(0.145 0 0);
 52 |   --popover: oklch(1 0 0);
 53 |   --popover-foreground: oklch(0.145 0 0);
 54 |   --primary: oklch(0.205 0 0);
 55 |   --primary-foreground: oklch(0.985 0 0);
 56 |   --secondary: oklch(0.97 0 0);
 57 |   --secondary-foreground: oklch(0.205 0 0);
 58 |   --muted: oklch(0.97 0 0);
 59 |   --muted-foreground: oklch(0.556 0 0);
 60 |   --accent: oklch(0.97 0 0);
 61 |   --accent-foreground: oklch(0.205 0 0);
 62 |   --destructive: oklch(0.577 0.245 27.325);
 63 |   --border: oklch(0.922 0 0);
 64 |   --input: oklch(0.922 0 0);
 65 |   --ring: oklch(0.708 0 0);
 66 |   --chart-1: oklch(0.646 0.222 41.116);
 67 |   --chart-2: oklch(0.6 0.118 184.704);
 68 |   --chart-3: oklch(0.398 0.07 227.392);
 69 |   --chart-4: oklch(0.828 0.189 84.429);
 70 |   --chart-5: oklch(0.769 0.188 70.08);
 71 |   --sidebar: oklch(0.985 0 0);
 72 |   --sidebar-foreground: oklch(0.145 0 0);
 73 |   --sidebar-primary: oklch(0.205 0 0);
 74 |   --sidebar-primary-foreground: oklch(0.985 0 0);
 75 |   --sidebar-accent: oklch(0.97 0 0);
 76 |   --sidebar-accent-foreground: oklch(0.205 0 0);
 77 |   --sidebar-border: oklch(0.922 0 0);
 78 |   --sidebar-ring: oklch(0.708 0 0);
 79 | }
 80 | 
 81 | .dark {
 82 |   --background: oklch(0.145 0 0);
 83 |   --foreground: oklch(0.985 0 0);
 84 |   --card: oklch(0.205 0 0);
 85 |   --card-foreground: oklch(0.985 0 0);
 86 |   --popover: oklch(0.205 0 0);
 87 |   --popover-foreground: oklch(0.985 0 0);
 88 |   --primary: oklch(0.922 0 0);
 89 |   --primary-foreground: oklch(0.205 0 0);
 90 |   --secondary: oklch(0.269 0 0);
 91 |   --secondary-foreground: oklch(0.985 0 0);
 92 |   --muted: oklch(0.269 0 0);
 93 |   --muted-foreground: oklch(0.708 0 0);
 94 |   --accent: oklch(0.269 0 0);
 95 |   --accent-foreground: oklch(0.985 0 0);
 96 |   --destructive: oklch(0.704 0.191 22.216);
 97 |   --border: oklch(1 0 0 / 10%);
 98 |   --input: oklch(1 0 0 / 15%);
 99 |   --ring: oklch(0.556 0 0);
100 |   --chart-1: oklch(0.488 0.243 264.376);
101 |   --chart-2: oklch(0.696 0.17 162.48);
102 |   --chart-3: oklch(0.769 0.188 70.08);
103 |   --chart-4: oklch(0.627 0.265 303.9);
104 |   --chart-5: oklch(0.645 0.246 16.439);
105 |   --sidebar: oklch(0.205 0 0);
106 |   --sidebar-foreground: oklch(0.985 0 0);
107 |   --sidebar-primary: oklch(0.488 0.243 264.376);
108 |   --sidebar-primary-foreground: oklch(0.985 0 0);
109 |   --sidebar-accent: oklch(0.269 0 0);
110 |   --sidebar-accent-foreground: oklch(0.985 0 0);
111 |   --sidebar-border: oklch(1 0 0 / 10%);
112 |   --sidebar-ring: oklch(0.556 0 0);
113 | }
114 | 
115 | @layer base {
116 |   * {
117 |     @apply border-border outline-ring/50;
118 |   }
119 |   body {
120 |     @apply bg-background text-foreground;
121 |   }
122 | }
123 | 


--------------------------------------------------------------------------------
/app/layout.tsx:
--------------------------------------------------------------------------------
 1 | import type { Metadata } from "next";
 2 | import "./globals.css";
 3 | import { UserProvider } from '@/context/userContext.js';
 4 | 
 5 | export const metadata: Metadata = {
 6 |   title: "Create Next App",
 7 |   description: "Generated by create next app",
 8 | };
 9 | 
10 | export default function RootLayout({
11 |   children,
12 | }: Readonly<{
13 |   children: React.ReactNode;
14 | }>) {
15 |   return (
16 |     <html lang="en">
17 |       <body
18 |         className={`antialiased`}
19 |       >
20 |         <UserProvider>
21 |           {children}
22 |         </UserProvider>
23 |       </body>
24 |     </html>
25 |   );
26 | }
27 | 


--------------------------------------------------------------------------------
/app/not-found.tsx:
--------------------------------------------------------------------------------
 1 | 'use client';
 2 | 
 3 | import React from 'react';
 4 | import Link from 'next/link';
 5 | 
 6 | export default function NotFound() {
 7 |   return (
 8 |     <div className='w-full h-screen flex flex-col items-center'>
 9 | 
10 |       <div className='w-10/12 h-full flex flex-col items-center justify-center text-2xl'>
11 |         <h1 className='text-3xl mb-4'>404 - Page Not Found</h1>
12 |         <p>Sorry, the page you are looking for does not exist.</p>
13 |         <Link href="/">
14 |           <p>Go back to the <span className='font-semibold transition-all hover:underline'>homepage</span>.</p>
15 |         </Link>
16 |       </div>
17 | 
18 |     </div>
19 |   );
20 | }


--------------------------------------------------------------------------------
/components.json:
--------------------------------------------------------------------------------
 1 | {
 2 |   "$schema": "https://ui.shadcn.com/schema.json",
 3 |   "style": "new-york",
 4 |   "rsc": true,
 5 |   "tsx": true,
 6 |   "tailwind": {
 7 |     "config": "",
 8 |     "css": "app/globals.css",
 9 |     "baseColor": "neutral",
10 |     "cssVariables": true,
11 |     "prefix": ""
12 |   },
13 |   "aliases": {
14 |     "components": "@/components",
15 |     "utils": "@/lib/utils",
16 |     "ui": "@/components/ui",
17 |     "lib": "@/lib",
18 |     "hooks": "@/hooks"
19 |   },
20 |   "iconLibrary": "lucide"
21 | }


--------------------------------------------------------------------------------
/components/common/Navbar.tsx:
--------------------------------------------------------------------------------
1 | import React from 'react'
2 | 
3 | const Navbar = () => {
4 |   return (
5 |     <div>Navbar</div>
6 |   )
7 | }
8 | 
9 | export default Navbar


--------------------------------------------------------------------------------
/components/ui/button.tsx:
--------------------------------------------------------------------------------
 1 | import * as React from "react"
 2 | import { Slot } from "@radix-ui/react-slot"
 3 | import { cva, type VariantProps } from "class-variance-authority"
 4 | 
 5 | import { cn } from "@/lib/utils"
 6 | 
 7 | const buttonVariants = cva(
 8 |   "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium transition-all disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4 shrink-0 [&_svg]:shrink-0 outline-none focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px] aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive",
 9 |   {
10 |     variants: {
11 |       variant: {
12 |         default:
13 |           "bg-primary text-primary-foreground shadow-xs hover:bg-primary/90",
14 |         destructive:
15 |           "bg-destructive text-white shadow-xs hover:bg-destructive/90 focus-visible:ring-destructive/20 dark:focus-visible:ring-destructive/40 dark:bg-destructive/60",
16 |         outline:
17 |           "border bg-background shadow-xs hover:bg-accent hover:text-accent-foreground dark:bg-input/30 dark:border-input dark:hover:bg-input/50",
18 |         secondary:
19 |           "bg-secondary text-secondary-foreground shadow-xs hover:bg-secondary/80",
20 |         ghost:
21 |           "hover:bg-accent hover:text-accent-foreground dark:hover:bg-accent/50",
22 |         link: "text-primary underline-offset-4 hover:underline",
23 |       },
24 |       size: {
25 |         default: "h-9 px-4 py-2 has-[>svg]:px-3",
26 |         sm: "h-8 rounded-md gap-1.5 px-3 has-[>svg]:px-2.5",
27 |         lg: "h-10 rounded-md px-6 has-[>svg]:px-4",
28 |         icon: "size-9",
29 |       },
30 |     },
31 |     defaultVariants: {
32 |       variant: "default",
33 |       size: "default",
34 |     },
35 |   }
36 | )
37 | 
38 | function Button({
39 |   className,
40 |   variant,
41 |   size,
42 |   asChild = false,
43 |   ...props
44 | }: React.ComponentProps<"button"> &
45 |   VariantProps<typeof buttonVariants> & {
46 |     asChild?: boolean
47 |   }) {
48 |   const Comp = asChild ? Slot : "button"
49 | 
50 |   return (
51 |     <Comp
52 |       data-slot="button"
53 |       className={cn(buttonVariants({ variant, size, className }))}
54 |       {...props}
55 |     />
56 |   )
57 | }
58 | 
59 | export { Button, buttonVariants }
60 | 


--------------------------------------------------------------------------------
/context/userContext.js:
--------------------------------------------------------------------------------
 1 | "use client";
 2 | import React, { createContext, useState } from "react";
 3 | 
 4 | export const UserContext = createContext();
 5 | 
 6 | export const UserProvider = ({ children }) => {
 7 |   const [loading, setLoading] = useState(false);
 8 | 
 9 |   return (
10 |     <UserContext.Provider
11 |       value={{
12 |         loading,
13 |         setLoading,
14 |       }}
15 |     >
16 |       {children}
17 |     </UserContext.Provider>
18 |   );
19 | };
20 | 


--------------------------------------------------------------------------------
/lib/utils.ts:
--------------------------------------------------------------------------------
1 | import { clsx, type ClassValue } from "clsx"
2 | import { twMerge } from "tailwind-merge"
3 | 
4 | export function cn(...inputs: ClassValue[]) {
5 |   return twMerge(clsx(inputs))
6 | }
7 | 


--------------------------------------------------------------------------------
/next.config.ts:
--------------------------------------------------------------------------------
1 | import type { NextConfig } from "next";
2 | 
3 | const nextConfig: NextConfig = {
4 |   /* config options here */
5 | };
6 | 
7 | export default nextConfig;
8 | 


--------------------------------------------------------------------------------
/package-lock.json:
--------------------------------------------------------------------------------
   1 | {
   2 |   "name": "nextjs-starters",
   3 |   "version": "0.1.0",
   4 |   "lockfileVersion": 3,
   5 |   "requires": true,
   6 |   "packages": {
   7 |     "": {
   8 |       "name": "nextjs-starters",
   9 |       "version": "0.1.0",
  10 |       "dependencies": {
  11 |         "@radix-ui/react-slot": "^1.2.3",
  12 |         "class-variance-authority": "^0.7.1",
  13 |         "clsx": "^2.1.1",
  14 |         "lucide-react": "^0.525.0",
  15 |         "next": "^15.5.2",
  16 |         "react": "^19.0.0",
  17 |         "react-dom": "^19.0.0",
  18 |         "tailwind-merge": "^3.3.1"
  19 |       },
  20 |       "devDependencies": {
  21 |         "@tailwindcss/postcss": "^4",
  22 |         "@types/node": "^20",
  23 |         "@types/react": "^19",
  24 |         "@types/react-dom": "^19",
  25 |         "tailwindcss": "^4",
  26 |         "tw-animate-css": "^1.3.5",
  27 |         "typescript": "^5"
  28 |       }
  29 |     },
  30 |     "node_modules/@alloc/quick-lru": {
  31 |       "version": "5.2.0",
  32 |       "resolved": "https://registry.npmjs.org/@alloc/quick-lru/-/quick-lru-5.2.0.tgz",
  33 |       "integrity": "sha512-UrcABB+4bUrFABwbluTIBErXwvbsU/V7TZWfmbgJfbkwiBuziS9gxdODUyuiecfdGQ85jglMW6juS3+z5TsKLw==",
  34 |       "dev": true,
  35 |       "license": "MIT",
  36 |       "engines": {
  37 |         "node": ">=10"
  38 |       },
  39 |       "funding": {
  40 |         "url": "https://github.com/sponsors/sindresorhus"
  41 |       }
  42 |     },
  43 |     "node_modules/@emnapi/runtime": {
  44 |       "version": "1.5.0",
  45 |       "resolved": "https://registry.npmjs.org/@emnapi/runtime/-/runtime-1.5.0.tgz",
  46 |       "integrity": "sha512-97/BJ3iXHww3djw6hYIfErCZFee7qCtrneuLa20UXFCOTCfBM2cvQHjWJ2EG0s0MtdNwInarqCTz35i4wWXHsQ==",
  47 |       "license": "MIT",
  48 |       "optional": true,
  49 |       "dependencies": {
  50 |         "tslib": "^2.4.0"
  51 |       }
  52 |     },
  53 |     "node_modules/@img/sharp-darwin-arm64": {
  54 |       "version": "0.34.3",
  55 |       "resolved": "https://registry.npmjs.org/@img/sharp-darwin-arm64/-/sharp-darwin-arm64-0.34.3.tgz",
  56 |       "integrity": "sha512-ryFMfvxxpQRsgZJqBd4wsttYQbCxsJksrv9Lw/v798JcQ8+w84mBWuXwl+TT0WJ/WrYOLaYpwQXi3sA9nTIaIg==",
  57 |       "cpu": [
  58 |         "arm64"
  59 |       ],
  60 |       "license": "Apache-2.0",
  61 |       "optional": true,
  62 |       "os": [
  63 |         "darwin"
  64 |       ],
  65 |       "engines": {
  66 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
  67 |       },
  68 |       "funding": {
  69 |         "url": "https://opencollective.com/libvips"
  70 |       },
  71 |       "optionalDependencies": {
  72 |         "@img/sharp-libvips-darwin-arm64": "1.2.0"
  73 |       }
  74 |     },
  75 |     "node_modules/@img/sharp-darwin-x64": {
  76 |       "version": "0.34.3",
  77 |       "resolved": "https://registry.npmjs.org/@img/sharp-darwin-x64/-/sharp-darwin-x64-0.34.3.tgz",
  78 |       "integrity": "sha512-yHpJYynROAj12TA6qil58hmPmAwxKKC7reUqtGLzsOHfP7/rniNGTL8tjWX6L3CTV4+5P4ypcS7Pp+7OB+8ihA==",
  79 |       "cpu": [
  80 |         "x64"
  81 |       ],
  82 |       "license": "Apache-2.0",
  83 |       "optional": true,
  84 |       "os": [
  85 |         "darwin"
  86 |       ],
  87 |       "engines": {
  88 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
  89 |       },
  90 |       "funding": {
  91 |         "url": "https://opencollective.com/libvips"
  92 |       },
  93 |       "optionalDependencies": {
  94 |         "@img/sharp-libvips-darwin-x64": "1.2.0"
  95 |       }
  96 |     },
  97 |     "node_modules/@img/sharp-libvips-darwin-arm64": {
  98 |       "version": "1.2.0",
  99 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-darwin-arm64/-/sharp-libvips-darwin-arm64-1.2.0.tgz",
 100 |       "integrity": "sha512-sBZmpwmxqwlqG9ueWFXtockhsxefaV6O84BMOrhtg/YqbTaRdqDE7hxraVE3y6gVM4eExmfzW4a8el9ArLeEiQ==",
 101 |       "cpu": [
 102 |         "arm64"
 103 |       ],
 104 |       "license": "LGPL-3.0-or-later",
 105 |       "optional": true,
 106 |       "os": [
 107 |         "darwin"
 108 |       ],
 109 |       "funding": {
 110 |         "url": "https://opencollective.com/libvips"
 111 |       }
 112 |     },
 113 |     "node_modules/@img/sharp-libvips-darwin-x64": {
 114 |       "version": "1.2.0",
 115 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-darwin-x64/-/sharp-libvips-darwin-x64-1.2.0.tgz",
 116 |       "integrity": "sha512-M64XVuL94OgiNHa5/m2YvEQI5q2cl9d/wk0qFTDVXcYzi43lxuiFTftMR1tOnFQovVXNZJ5TURSDK2pNe9Yzqg==",
 117 |       "cpu": [
 118 |         "x64"
 119 |       ],
 120 |       "license": "LGPL-3.0-or-later",
 121 |       "optional": true,
 122 |       "os": [
 123 |         "darwin"
 124 |       ],
 125 |       "funding": {
 126 |         "url": "https://opencollective.com/libvips"
 127 |       }
 128 |     },
 129 |     "node_modules/@img/sharp-libvips-linux-arm": {
 130 |       "version": "1.2.0",
 131 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linux-arm/-/sharp-libvips-linux-arm-1.2.0.tgz",
 132 |       "integrity": "sha512-mWd2uWvDtL/nvIzThLq3fr2nnGfyr/XMXlq8ZJ9WMR6PXijHlC3ksp0IpuhK6bougvQrchUAfzRLnbsen0Cqvw==",
 133 |       "cpu": [
 134 |         "arm"
 135 |       ],
 136 |       "license": "LGPL-3.0-or-later",
 137 |       "optional": true,
 138 |       "os": [
 139 |         "linux"
 140 |       ],
 141 |       "funding": {
 142 |         "url": "https://opencollective.com/libvips"
 143 |       }
 144 |     },
 145 |     "node_modules/@img/sharp-libvips-linux-arm64": {
 146 |       "version": "1.2.0",
 147 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linux-arm64/-/sharp-libvips-linux-arm64-1.2.0.tgz",
 148 |       "integrity": "sha512-RXwd0CgG+uPRX5YYrkzKyalt2OJYRiJQ8ED/fi1tq9WQW2jsQIn0tqrlR5l5dr/rjqq6AHAxURhj2DVjyQWSOA==",
 149 |       "cpu": [
 150 |         "arm64"
 151 |       ],
 152 |       "license": "LGPL-3.0-or-later",
 153 |       "optional": true,
 154 |       "os": [
 155 |         "linux"
 156 |       ],
 157 |       "funding": {
 158 |         "url": "https://opencollective.com/libvips"
 159 |       }
 160 |     },
 161 |     "node_modules/@img/sharp-libvips-linux-ppc64": {
 162 |       "version": "1.2.0",
 163 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linux-ppc64/-/sharp-libvips-linux-ppc64-1.2.0.tgz",
 164 |       "integrity": "sha512-Xod/7KaDDHkYu2phxxfeEPXfVXFKx70EAFZ0qyUdOjCcxbjqyJOEUpDe6RIyaunGxT34Anf9ue/wuWOqBW2WcQ==",
 165 |       "cpu": [
 166 |         "ppc64"
 167 |       ],
 168 |       "license": "LGPL-3.0-or-later",
 169 |       "optional": true,
 170 |       "os": [
 171 |         "linux"
 172 |       ],
 173 |       "funding": {
 174 |         "url": "https://opencollective.com/libvips"
 175 |       }
 176 |     },
 177 |     "node_modules/@img/sharp-libvips-linux-s390x": {
 178 |       "version": "1.2.0",
 179 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linux-s390x/-/sharp-libvips-linux-s390x-1.2.0.tgz",
 180 |       "integrity": "sha512-eMKfzDxLGT8mnmPJTNMcjfO33fLiTDsrMlUVcp6b96ETbnJmd4uvZxVJSKPQfS+odwfVaGifhsB07J1LynFehw==",
 181 |       "cpu": [
 182 |         "s390x"
 183 |       ],
 184 |       "license": "LGPL-3.0-or-later",
 185 |       "optional": true,
 186 |       "os": [
 187 |         "linux"
 188 |       ],
 189 |       "funding": {
 190 |         "url": "https://opencollective.com/libvips"
 191 |       }
 192 |     },
 193 |     "node_modules/@img/sharp-libvips-linux-x64": {
 194 |       "version": "1.2.0",
 195 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linux-x64/-/sharp-libvips-linux-x64-1.2.0.tgz",
 196 |       "integrity": "sha512-ZW3FPWIc7K1sH9E3nxIGB3y3dZkpJlMnkk7z5tu1nSkBoCgw2nSRTFHI5pB/3CQaJM0pdzMF3paf9ckKMSE9Tg==",
 197 |       "cpu": [
 198 |         "x64"
 199 |       ],
 200 |       "license": "LGPL-3.0-or-later",
 201 |       "optional": true,
 202 |       "os": [
 203 |         "linux"
 204 |       ],
 205 |       "funding": {
 206 |         "url": "https://opencollective.com/libvips"
 207 |       }
 208 |     },
 209 |     "node_modules/@img/sharp-libvips-linuxmusl-arm64": {
 210 |       "version": "1.2.0",
 211 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linuxmusl-arm64/-/sharp-libvips-linuxmusl-arm64-1.2.0.tgz",
 212 |       "integrity": "sha512-UG+LqQJbf5VJ8NWJ5Z3tdIe/HXjuIdo4JeVNADXBFuG7z9zjoegpzzGIyV5zQKi4zaJjnAd2+g2nna8TZvuW9Q==",
 213 |       "cpu": [
 214 |         "arm64"
 215 |       ],
 216 |       "license": "LGPL-3.0-or-later",
 217 |       "optional": true,
 218 |       "os": [
 219 |         "linux"
 220 |       ],
 221 |       "funding": {
 222 |         "url": "https://opencollective.com/libvips"
 223 |       }
 224 |     },
 225 |     "node_modules/@img/sharp-libvips-linuxmusl-x64": {
 226 |       "version": "1.2.0",
 227 |       "resolved": "https://registry.npmjs.org/@img/sharp-libvips-linuxmusl-x64/-/sharp-libvips-linuxmusl-x64-1.2.0.tgz",
 228 |       "integrity": "sha512-SRYOLR7CXPgNze8akZwjoGBoN1ThNZoqpOgfnOxmWsklTGVfJiGJoC/Lod7aNMGA1jSsKWM1+HRX43OP6p9+6Q==",
 229 |       "cpu": [
 230 |         "x64"
 231 |       ],
 232 |       "license": "LGPL-3.0-or-later",
 233 |       "optional": true,
 234 |       "os": [
 235 |         "linux"
 236 |       ],
 237 |       "funding": {
 238 |         "url": "https://opencollective.com/libvips"
 239 |       }
 240 |     },
 241 |     "node_modules/@img/sharp-linux-arm": {
 242 |       "version": "0.34.3",
 243 |       "resolved": "https://registry.npmjs.org/@img/sharp-linux-arm/-/sharp-linux-arm-0.34.3.tgz",
 244 |       "integrity": "sha512-oBK9l+h6KBN0i3dC8rYntLiVfW8D8wH+NPNT3O/WBHeW0OQWCjfWksLUaPidsrDKpJgXp3G3/hkmhptAW0I3+A==",
 245 |       "cpu": [
 246 |         "arm"
 247 |       ],
 248 |       "license": "Apache-2.0",
 249 |       "optional": true,
 250 |       "os": [
 251 |         "linux"
 252 |       ],
 253 |       "engines": {
 254 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 255 |       },
 256 |       "funding": {
 257 |         "url": "https://opencollective.com/libvips"
 258 |       },
 259 |       "optionalDependencies": {
 260 |         "@img/sharp-libvips-linux-arm": "1.2.0"
 261 |       }
 262 |     },
 263 |     "node_modules/@img/sharp-linux-arm64": {
 264 |       "version": "0.34.3",
 265 |       "resolved": "https://registry.npmjs.org/@img/sharp-linux-arm64/-/sharp-linux-arm64-0.34.3.tgz",
 266 |       "integrity": "sha512-QdrKe3EvQrqwkDrtuTIjI0bu6YEJHTgEeqdzI3uWJOH6G1O8Nl1iEeVYRGdj1h5I21CqxSvQp1Yv7xeU3ZewbA==",
 267 |       "cpu": [
 268 |         "arm64"
 269 |       ],
 270 |       "license": "Apache-2.0",
 271 |       "optional": true,
 272 |       "os": [
 273 |         "linux"
 274 |       ],
 275 |       "engines": {
 276 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 277 |       },
 278 |       "funding": {
 279 |         "url": "https://opencollective.com/libvips"
 280 |       },
 281 |       "optionalDependencies": {
 282 |         "@img/sharp-libvips-linux-arm64": "1.2.0"
 283 |       }
 284 |     },
 285 |     "node_modules/@img/sharp-linux-ppc64": {
 286 |       "version": "0.34.3",
 287 |       "resolved": "https://registry.npmjs.org/@img/sharp-linux-ppc64/-/sharp-linux-ppc64-0.34.3.tgz",
 288 |       "integrity": "sha512-GLtbLQMCNC5nxuImPR2+RgrviwKwVql28FWZIW1zWruy6zLgA5/x2ZXk3mxj58X/tszVF69KK0Is83V8YgWhLA==",
 289 |       "cpu": [
 290 |         "ppc64"
 291 |       ],
 292 |       "license": "Apache-2.0",
 293 |       "optional": true,
 294 |       "os": [
 295 |         "linux"
 296 |       ],
 297 |       "engines": {
 298 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 299 |       },
 300 |       "funding": {
 301 |         "url": "https://opencollective.com/libvips"
 302 |       },
 303 |       "optionalDependencies": {
 304 |         "@img/sharp-libvips-linux-ppc64": "1.2.0"
 305 |       }
 306 |     },
 307 |     "node_modules/@img/sharp-linux-s390x": {
 308 |       "version": "0.34.3",
 309 |       "resolved": "https://registry.npmjs.org/@img/sharp-linux-s390x/-/sharp-linux-s390x-0.34.3.tgz",
 310 |       "integrity": "sha512-3gahT+A6c4cdc2edhsLHmIOXMb17ltffJlxR0aC2VPZfwKoTGZec6u5GrFgdR7ciJSsHT27BD3TIuGcuRT0KmQ==",
 311 |       "cpu": [
 312 |         "s390x"
 313 |       ],
 314 |       "license": "Apache-2.0",
 315 |       "optional": true,
 316 |       "os": [
 317 |         "linux"
 318 |       ],
 319 |       "engines": {
 320 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 321 |       },
 322 |       "funding": {
 323 |         "url": "https://opencollective.com/libvips"
 324 |       },
 325 |       "optionalDependencies": {
 326 |         "@img/sharp-libvips-linux-s390x": "1.2.0"
 327 |       }
 328 |     },
 329 |     "node_modules/@img/sharp-linux-x64": {
 330 |       "version": "0.34.3",
 331 |       "resolved": "https://registry.npmjs.org/@img/sharp-linux-x64/-/sharp-linux-x64-0.34.3.tgz",
 332 |       "integrity": "sha512-8kYso8d806ypnSq3/Ly0QEw90V5ZoHh10yH0HnrzOCr6DKAPI6QVHvwleqMkVQ0m+fc7EH8ah0BB0QPuWY6zJQ==",
 333 |       "cpu": [
 334 |         "x64"
 335 |       ],
 336 |       "license": "Apache-2.0",
 337 |       "optional": true,
 338 |       "os": [
 339 |         "linux"
 340 |       ],
 341 |       "engines": {
 342 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 343 |       },
 344 |       "funding": {
 345 |         "url": "https://opencollective.com/libvips"
 346 |       },
 347 |       "optionalDependencies": {
 348 |         "@img/sharp-libvips-linux-x64": "1.2.0"
 349 |       }
 350 |     },
 351 |     "node_modules/@img/sharp-linuxmusl-arm64": {
 352 |       "version": "0.34.3",
 353 |       "resolved": "https://registry.npmjs.org/@img/sharp-linuxmusl-arm64/-/sharp-linuxmusl-arm64-0.34.3.tgz",
 354 |       "integrity": "sha512-vAjbHDlr4izEiXM1OTggpCcPg9tn4YriK5vAjowJsHwdBIdx0fYRsURkxLG2RLm9gyBq66gwtWI8Gx0/ov+JKQ==",
 355 |       "cpu": [
 356 |         "arm64"
 357 |       ],
 358 |       "license": "Apache-2.0",
 359 |       "optional": true,
 360 |       "os": [
 361 |         "linux"
 362 |       ],
 363 |       "engines": {
 364 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 365 |       },
 366 |       "funding": {
 367 |         "url": "https://opencollective.com/libvips"
 368 |       },
 369 |       "optionalDependencies": {
 370 |         "@img/sharp-libvips-linuxmusl-arm64": "1.2.0"
 371 |       }
 372 |     },
 373 |     "node_modules/@img/sharp-linuxmusl-x64": {
 374 |       "version": "0.34.3",
 375 |       "resolved": "https://registry.npmjs.org/@img/sharp-linuxmusl-x64/-/sharp-linuxmusl-x64-0.34.3.tgz",
 376 |       "integrity": "sha512-gCWUn9547K5bwvOn9l5XGAEjVTTRji4aPTqLzGXHvIr6bIDZKNTA34seMPgM0WmSf+RYBH411VavCejp3PkOeQ==",
 377 |       "cpu": [
 378 |         "x64"
 379 |       ],
 380 |       "license": "Apache-2.0",
 381 |       "optional": true,
 382 |       "os": [
 383 |         "linux"
 384 |       ],
 385 |       "engines": {
 386 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 387 |       },
 388 |       "funding": {
 389 |         "url": "https://opencollective.com/libvips"
 390 |       },
 391 |       "optionalDependencies": {
 392 |         "@img/sharp-libvips-linuxmusl-x64": "1.2.0"
 393 |       }
 394 |     },
 395 |     "node_modules/@img/sharp-wasm32": {
 396 |       "version": "0.34.3",
 397 |       "resolved": "https://registry.npmjs.org/@img/sharp-wasm32/-/sharp-wasm32-0.34.3.tgz",
 398 |       "integrity": "sha512-+CyRcpagHMGteySaWos8IbnXcHgfDn7pO2fiC2slJxvNq9gDipYBN42/RagzctVRKgxATmfqOSulgZv5e1RdMg==",
 399 |       "cpu": [
 400 |         "wasm32"
 401 |       ],
 402 |       "license": "Apache-2.0 AND LGPL-3.0-or-later AND MIT",
 403 |       "optional": true,
 404 |       "dependencies": {
 405 |         "@emnapi/runtime": "^1.4.4"
 406 |       },
 407 |       "engines": {
 408 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 409 |       },
 410 |       "funding": {
 411 |         "url": "https://opencollective.com/libvips"
 412 |       }
 413 |     },
 414 |     "node_modules/@img/sharp-win32-arm64": {
 415 |       "version": "0.34.3",
 416 |       "resolved": "https://registry.npmjs.org/@img/sharp-win32-arm64/-/sharp-win32-arm64-0.34.3.tgz",
 417 |       "integrity": "sha512-MjnHPnbqMXNC2UgeLJtX4XqoVHHlZNd+nPt1kRPmj63wURegwBhZlApELdtxM2OIZDRv/DFtLcNhVbd1z8GYXQ==",
 418 |       "cpu": [
 419 |         "arm64"
 420 |       ],
 421 |       "license": "Apache-2.0 AND LGPL-3.0-or-later",
 422 |       "optional": true,
 423 |       "os": [
 424 |         "win32"
 425 |       ],
 426 |       "engines": {
 427 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 428 |       },
 429 |       "funding": {
 430 |         "url": "https://opencollective.com/libvips"
 431 |       }
 432 |     },
 433 |     "node_modules/@img/sharp-win32-ia32": {
 434 |       "version": "0.34.3",
 435 |       "resolved": "https://registry.npmjs.org/@img/sharp-win32-ia32/-/sharp-win32-ia32-0.34.3.tgz",
 436 |       "integrity": "sha512-xuCdhH44WxuXgOM714hn4amodJMZl3OEvf0GVTm0BEyMeA2to+8HEdRPShH0SLYptJY1uBw+SCFP9WVQi1Q/cw==",
 437 |       "cpu": [
 438 |         "ia32"
 439 |       ],
 440 |       "license": "Apache-2.0 AND LGPL-3.0-or-later",
 441 |       "optional": true,
 442 |       "os": [
 443 |         "win32"
 444 |       ],
 445 |       "engines": {
 446 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 447 |       },
 448 |       "funding": {
 449 |         "url": "https://opencollective.com/libvips"
 450 |       }
 451 |     },
 452 |     "node_modules/@img/sharp-win32-x64": {
 453 |       "version": "0.34.3",
 454 |       "resolved": "https://registry.npmjs.org/@img/sharp-win32-x64/-/sharp-win32-x64-0.34.3.tgz",
 455 |       "integrity": "sha512-OWwz05d++TxzLEv4VnsTz5CmZ6mI6S05sfQGEMrNrQcOEERbX46332IvE7pO/EUiw7jUrrS40z/M7kPyjfl04g==",
 456 |       "cpu": [
 457 |         "x64"
 458 |       ],
 459 |       "license": "Apache-2.0 AND LGPL-3.0-or-later",
 460 |       "optional": true,
 461 |       "os": [
 462 |         "win32"
 463 |       ],
 464 |       "engines": {
 465 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
 466 |       },
 467 |       "funding": {
 468 |         "url": "https://opencollective.com/libvips"
 469 |       }
 470 |     },
 471 |     "node_modules/@isaacs/fs-minipass": {
 472 |       "version": "4.0.1",
 473 |       "resolved": "https://registry.npmjs.org/@isaacs/fs-minipass/-/fs-minipass-4.0.1.tgz",
 474 |       "integrity": "sha512-wgm9Ehl2jpeqP3zw/7mo3kRHFp5MEDhqAdwy1fTGkHAwnkGOVsgpvQhL8B5n1qlb01jV3n/bI0ZfZp5lWA1k4w==",
 475 |       "dev": true,
 476 |       "license": "ISC",
 477 |       "dependencies": {
 478 |         "minipass": "^7.0.4"
 479 |       },
 480 |       "engines": {
 481 |         "node": ">=18.0.0"
 482 |       }
 483 |     },
 484 |     "node_modules/@jridgewell/gen-mapping": {
 485 |       "version": "0.3.13",
 486 |       "resolved": "https://registry.npmjs.org/@jridgewell/gen-mapping/-/gen-mapping-0.3.13.tgz",
 487 |       "integrity": "sha512-2kkt/7niJ6MgEPxF0bYdQ6etZaA+fQvDcLKckhy1yIQOzaoKjBBjSj63/aLVjYE3qhRt5dvM+uUyfCg6UKCBbA==",
 488 |       "dev": true,
 489 |       "license": "MIT",
 490 |       "dependencies": {
 491 |         "@jridgewell/sourcemap-codec": "^1.5.0",
 492 |         "@jridgewell/trace-mapping": "^0.3.24"
 493 |       }
 494 |     },
 495 |     "node_modules/@jridgewell/remapping": {
 496 |       "version": "2.3.5",
 497 |       "resolved": "https://registry.npmjs.org/@jridgewell/remapping/-/remapping-2.3.5.tgz",
 498 |       "integrity": "sha512-LI9u/+laYG4Ds1TDKSJW2YPrIlcVYOwi2fUC6xB43lueCjgxV4lffOCZCtYFiH6TNOX+tQKXx97T4IKHbhyHEQ==",
 499 |       "dev": true,
 500 |       "license": "MIT",
 501 |       "dependencies": {
 502 |         "@jridgewell/gen-mapping": "^0.3.5",
 503 |         "@jridgewell/trace-mapping": "^0.3.24"
 504 |       }
 505 |     },
 506 |     "node_modules/@jridgewell/resolve-uri": {
 507 |       "version": "3.1.2",
 508 |       "resolved": "https://registry.npmjs.org/@jridgewell/resolve-uri/-/resolve-uri-3.1.2.tgz",
 509 |       "integrity": "sha512-bRISgCIjP20/tbWSPWMEi54QVPRZExkuD9lJL+UIxUKtwVJA8wW1Trb1jMs1RFXo1CBTNZ/5hpC9QvmKWdopKw==",
 510 |       "dev": true,
 511 |       "license": "MIT",
 512 |       "engines": {
 513 |         "node": ">=6.0.0"
 514 |       }
 515 |     },
 516 |     "node_modules/@jridgewell/sourcemap-codec": {
 517 |       "version": "1.5.5",
 518 |       "resolved": "https://registry.npmjs.org/@jridgewell/sourcemap-codec/-/sourcemap-codec-1.5.5.tgz",
 519 |       "integrity": "sha512-cYQ9310grqxueWbl+WuIUIaiUaDcj7WOq5fVhEljNVgRfOUhY9fy2zTvfoqWsnebh8Sl70VScFbICvJnLKB0Og==",
 520 |       "dev": true,
 521 |       "license": "MIT"
 522 |     },
 523 |     "node_modules/@jridgewell/trace-mapping": {
 524 |       "version": "0.3.30",
 525 |       "resolved": "https://registry.npmjs.org/@jridgewell/trace-mapping/-/trace-mapping-0.3.30.tgz",
 526 |       "integrity": "sha512-GQ7Nw5G2lTu/BtHTKfXhKHok2WGetd4XYcVKGx00SjAk8GMwgJM3zr6zORiPGuOE+/vkc90KtTosSSvaCjKb2Q==",
 527 |       "dev": true,
 528 |       "license": "MIT",
 529 |       "dependencies": {
 530 |         "@jridgewell/resolve-uri": "^3.1.0",
 531 |         "@jridgewell/sourcemap-codec": "^1.4.14"
 532 |       }
 533 |     },
 534 |     "node_modules/@next/env": {
 535 |       "version": "15.5.2",
 536 |       "resolved": "https://registry.npmjs.org/@next/env/-/env-15.5.2.tgz",
 537 |       "integrity": "sha512-Qe06ew4zt12LeO6N7j8/nULSOe3fMXE4dM6xgpBQNvdzyK1sv5y4oAP3bq4LamrvGCZtmRYnW8URFCeX5nFgGg==",
 538 |       "license": "MIT"
 539 |     },
 540 |     "node_modules/@next/swc-darwin-arm64": {
 541 |       "version": "15.5.2",
 542 |       "resolved": "https://registry.npmjs.org/@next/swc-darwin-arm64/-/swc-darwin-arm64-15.5.2.tgz",
 543 |       "integrity": "sha512-8bGt577BXGSd4iqFygmzIfTYizHb0LGWqH+qgIF/2EDxS5JsSdERJKA8WgwDyNBZgTIIA4D8qUtoQHmxIIquoQ==",
 544 |       "cpu": [
 545 |         "arm64"
 546 |       ],
 547 |       "license": "MIT",
 548 |       "optional": true,
 549 |       "os": [
 550 |         "darwin"
 551 |       ],
 552 |       "engines": {
 553 |         "node": ">= 10"
 554 |       }
 555 |     },
 556 |     "node_modules/@next/swc-darwin-x64": {
 557 |       "version": "15.5.2",
 558 |       "resolved": "https://registry.npmjs.org/@next/swc-darwin-x64/-/swc-darwin-x64-15.5.2.tgz",
 559 |       "integrity": "sha512-2DjnmR6JHK4X+dgTXt5/sOCu/7yPtqpYt8s8hLkHFK3MGkka2snTv3yRMdHvuRtJVkPwCGsvBSwmoQCHatauFQ==",
 560 |       "cpu": [
 561 |         "x64"
 562 |       ],
 563 |       "license": "MIT",
 564 |       "optional": true,
 565 |       "os": [
 566 |         "darwin"
 567 |       ],
 568 |       "engines": {
 569 |         "node": ">= 10"
 570 |       }
 571 |     },
 572 |     "node_modules/@next/swc-linux-arm64-gnu": {
 573 |       "version": "15.5.2",
 574 |       "resolved": "https://registry.npmjs.org/@next/swc-linux-arm64-gnu/-/swc-linux-arm64-gnu-15.5.2.tgz",
 575 |       "integrity": "sha512-3j7SWDBS2Wov/L9q0mFJtEvQ5miIqfO4l7d2m9Mo06ddsgUK8gWfHGgbjdFlCp2Ek7MmMQZSxpGFqcC8zGh2AA==",
 576 |       "cpu": [
 577 |         "arm64"
 578 |       ],
 579 |       "license": "MIT",
 580 |       "optional": true,
 581 |       "os": [
 582 |         "linux"
 583 |       ],
 584 |       "engines": {
 585 |         "node": ">= 10"
 586 |       }
 587 |     },
 588 |     "node_modules/@next/swc-linux-arm64-musl": {
 589 |       "version": "15.5.2",
 590 |       "resolved": "https://registry.npmjs.org/@next/swc-linux-arm64-musl/-/swc-linux-arm64-musl-15.5.2.tgz",
 591 |       "integrity": "sha512-s6N8k8dF9YGc5T01UPQ08yxsK6fUow5gG1/axWc1HVVBYQBgOjca4oUZF7s4p+kwhkB1bDSGR8QznWrFZ/Rt5g==",
 592 |       "cpu": [
 593 |         "arm64"
 594 |       ],
 595 |       "license": "MIT",
 596 |       "optional": true,
 597 |       "os": [
 598 |         "linux"
 599 |       ],
 600 |       "engines": {
 601 |         "node": ">= 10"
 602 |       }
 603 |     },
 604 |     "node_modules/@next/swc-linux-x64-gnu": {
 605 |       "version": "15.5.2",
 606 |       "resolved": "https://registry.npmjs.org/@next/swc-linux-x64-gnu/-/swc-linux-x64-gnu-15.5.2.tgz",
 607 |       "integrity": "sha512-o1RV/KOODQh6dM6ZRJGZbc+MOAHww33Vbs5JC9Mp1gDk8cpEO+cYC/l7rweiEalkSm5/1WGa4zY7xrNwObN4+Q==",
 608 |       "cpu": [
 609 |         "x64"
 610 |       ],
 611 |       "license": "MIT",
 612 |       "optional": true,
 613 |       "os": [
 614 |         "linux"
 615 |       ],
 616 |       "engines": {
 617 |         "node": ">= 10"
 618 |       }
 619 |     },
 620 |     "node_modules/@next/swc-linux-x64-musl": {
 621 |       "version": "15.5.2",
 622 |       "resolved": "https://registry.npmjs.org/@next/swc-linux-x64-musl/-/swc-linux-x64-musl-15.5.2.tgz",
 623 |       "integrity": "sha512-/VUnh7w8RElYZ0IV83nUcP/J4KJ6LLYliiBIri3p3aW2giF+PAVgZb6mk8jbQSB3WlTai8gEmCAr7kptFa1H6g==",
 624 |       "cpu": [
 625 |         "x64"
 626 |       ],
 627 |       "license": "MIT",
 628 |       "optional": true,
 629 |       "os": [
 630 |         "linux"
 631 |       ],
 632 |       "engines": {
 633 |         "node": ">= 10"
 634 |       }
 635 |     },
 636 |     "node_modules/@next/swc-win32-arm64-msvc": {
 637 |       "version": "15.5.2",
 638 |       "resolved": "https://registry.npmjs.org/@next/swc-win32-arm64-msvc/-/swc-win32-arm64-msvc-15.5.2.tgz",
 639 |       "integrity": "sha512-sMPyTvRcNKXseNQ/7qRfVRLa0VhR0esmQ29DD6pqvG71+JdVnESJaHPA8t7bc67KD5spP3+DOCNLhqlEI2ZgQg==",
 640 |       "cpu": [
 641 |         "arm64"
 642 |       ],
 643 |       "license": "MIT",
 644 |       "optional": true,
 645 |       "os": [
 646 |         "win32"
 647 |       ],
 648 |       "engines": {
 649 |         "node": ">= 10"
 650 |       }
 651 |     },
 652 |     "node_modules/@next/swc-win32-x64-msvc": {
 653 |       "version": "15.5.2",
 654 |       "resolved": "https://registry.npmjs.org/@next/swc-win32-x64-msvc/-/swc-win32-x64-msvc-15.5.2.tgz",
 655 |       "integrity": "sha512-W5VvyZHnxG/2ukhZF/9Ikdra5fdNftxI6ybeVKYvBPDtyx7x4jPPSNduUkfH5fo3zG0JQ0bPxgy41af2JX5D4Q==",
 656 |       "cpu": [
 657 |         "x64"
 658 |       ],
 659 |       "license": "MIT",
 660 |       "optional": true,
 661 |       "os": [
 662 |         "win32"
 663 |       ],
 664 |       "engines": {
 665 |         "node": ">= 10"
 666 |       }
 667 |     },
 668 |     "node_modules/@radix-ui/react-compose-refs": {
 669 |       "version": "1.1.2",
 670 |       "resolved": "https://registry.npmjs.org/@radix-ui/react-compose-refs/-/react-compose-refs-1.1.2.tgz",
 671 |       "integrity": "sha512-z4eqJvfiNnFMHIIvXP3CY57y2WJs5g2v3X0zm9mEJkrkNv4rDxu+sg9Jh8EkXyeqBkB7SOcboo9dMVqhyrACIg==",
 672 |       "license": "MIT",
 673 |       "peerDependencies": {
 674 |         "@types/react": "*",
 675 |         "react": "^16.8 || ^17.0 || ^18.0 || ^19.0 || ^19.0.0-rc"
 676 |       },
 677 |       "peerDependenciesMeta": {
 678 |         "@types/react": {
 679 |           "optional": true
 680 |         }
 681 |       }
 682 |     },
 683 |     "node_modules/@radix-ui/react-slot": {
 684 |       "version": "1.2.3",
 685 |       "resolved": "https://registry.npmjs.org/@radix-ui/react-slot/-/react-slot-1.2.3.tgz",
 686 |       "integrity": "sha512-aeNmHnBxbi2St0au6VBVC7JXFlhLlOnvIIlePNniyUNAClzmtAUEY8/pBiK3iHjufOlwA+c20/8jngo7xcrg8A==",
 687 |       "license": "MIT",
 688 |       "dependencies": {
 689 |         "@radix-ui/react-compose-refs": "1.1.2"
 690 |       },
 691 |       "peerDependencies": {
 692 |         "@types/react": "*",
 693 |         "react": "^16.8 || ^17.0 || ^18.0 || ^19.0 || ^19.0.0-rc"
 694 |       },
 695 |       "peerDependenciesMeta": {
 696 |         "@types/react": {
 697 |           "optional": true
 698 |         }
 699 |       }
 700 |     },
 701 |     "node_modules/@swc/helpers": {
 702 |       "version": "0.5.15",
 703 |       "resolved": "https://registry.npmjs.org/@swc/helpers/-/helpers-0.5.15.tgz",
 704 |       "integrity": "sha512-JQ5TuMi45Owi4/BIMAJBoSQoOJu12oOk/gADqlcUL9JEdHB8vyjUSsxqeNXnmXHjYKMi2WcYtezGEEhqUI/E2g==",
 705 |       "license": "Apache-2.0",
 706 |       "dependencies": {
 707 |         "tslib": "^2.8.0"
 708 |       }
 709 |     },
 710 |     "node_modules/@tailwindcss/node": {
 711 |       "version": "4.1.13",
 712 |       "resolved": "https://registry.npmjs.org/@tailwindcss/node/-/node-4.1.13.tgz",
 713 |       "integrity": "sha512-eq3ouolC1oEFOAvOMOBAmfCIqZBJuvWvvYWh5h5iOYfe1HFC6+GZ6EIL0JdM3/niGRJmnrOc+8gl9/HGUaaptw==",
 714 |       "dev": true,
 715 |       "license": "MIT",
 716 |       "dependencies": {
 717 |         "@jridgewell/remapping": "^2.3.4",
 718 |         "enhanced-resolve": "^5.18.3",
 719 |         "jiti": "^2.5.1",
 720 |         "lightningcss": "1.30.1",
 721 |         "magic-string": "^0.30.18",
 722 |         "source-map-js": "^1.2.1",
 723 |         "tailwindcss": "4.1.13"
 724 |       }
 725 |     },
 726 |     "node_modules/@tailwindcss/oxide": {
 727 |       "version": "4.1.13",
 728 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide/-/oxide-4.1.13.tgz",
 729 |       "integrity": "sha512-CPgsM1IpGRa880sMbYmG1s4xhAy3xEt1QULgTJGQmZUeNgXFR7s1YxYygmJyBGtou4SyEosGAGEeYqY7R53bIA==",
 730 |       "dev": true,
 731 |       "hasInstallScript": true,
 732 |       "license": "MIT",
 733 |       "dependencies": {
 734 |         "detect-libc": "^2.0.4",
 735 |         "tar": "^7.4.3"
 736 |       },
 737 |       "engines": {
 738 |         "node": ">= 10"
 739 |       },
 740 |       "optionalDependencies": {
 741 |         "@tailwindcss/oxide-android-arm64": "4.1.13",
 742 |         "@tailwindcss/oxide-darwin-arm64": "4.1.13",
 743 |         "@tailwindcss/oxide-darwin-x64": "4.1.13",
 744 |         "@tailwindcss/oxide-freebsd-x64": "4.1.13",
 745 |         "@tailwindcss/oxide-linux-arm-gnueabihf": "4.1.13",
 746 |         "@tailwindcss/oxide-linux-arm64-gnu": "4.1.13",
 747 |         "@tailwindcss/oxide-linux-arm64-musl": "4.1.13",
 748 |         "@tailwindcss/oxide-linux-x64-gnu": "4.1.13",
 749 |         "@tailwindcss/oxide-linux-x64-musl": "4.1.13",
 750 |         "@tailwindcss/oxide-wasm32-wasi": "4.1.13",
 751 |         "@tailwindcss/oxide-win32-arm64-msvc": "4.1.13",
 752 |         "@tailwindcss/oxide-win32-x64-msvc": "4.1.13"
 753 |       }
 754 |     },
 755 |     "node_modules/@tailwindcss/oxide-android-arm64": {
 756 |       "version": "4.1.13",
 757 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-android-arm64/-/oxide-android-arm64-4.1.13.tgz",
 758 |       "integrity": "sha512-BrpTrVYyejbgGo57yc8ieE+D6VT9GOgnNdmh5Sac6+t0m+v+sKQevpFVpwX3pBrM2qKrQwJ0c5eDbtjouY/+ew==",
 759 |       "cpu": [
 760 |         "arm64"
 761 |       ],
 762 |       "dev": true,
 763 |       "license": "MIT",
 764 |       "optional": true,
 765 |       "os": [
 766 |         "android"
 767 |       ],
 768 |       "engines": {
 769 |         "node": ">= 10"
 770 |       }
 771 |     },
 772 |     "node_modules/@tailwindcss/oxide-darwin-arm64": {
 773 |       "version": "4.1.13",
 774 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-darwin-arm64/-/oxide-darwin-arm64-4.1.13.tgz",
 775 |       "integrity": "sha512-YP+Jksc4U0KHcu76UhRDHq9bx4qtBftp9ShK/7UGfq0wpaP96YVnnjFnj3ZFrUAjc5iECzODl/Ts0AN7ZPOANQ==",
 776 |       "cpu": [
 777 |         "arm64"
 778 |       ],
 779 |       "dev": true,
 780 |       "license": "MIT",
 781 |       "optional": true,
 782 |       "os": [
 783 |         "darwin"
 784 |       ],
 785 |       "engines": {
 786 |         "node": ">= 10"
 787 |       }
 788 |     },
 789 |     "node_modules/@tailwindcss/oxide-darwin-x64": {
 790 |       "version": "4.1.13",
 791 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-darwin-x64/-/oxide-darwin-x64-4.1.13.tgz",
 792 |       "integrity": "sha512-aAJ3bbwrn/PQHDxCto9sxwQfT30PzyYJFG0u/BWZGeVXi5Hx6uuUOQEI2Fa43qvmUjTRQNZnGqe9t0Zntexeuw==",
 793 |       "cpu": [
 794 |         "x64"
 795 |       ],
 796 |       "dev": true,
 797 |       "license": "MIT",
 798 |       "optional": true,
 799 |       "os": [
 800 |         "darwin"
 801 |       ],
 802 |       "engines": {
 803 |         "node": ">= 10"
 804 |       }
 805 |     },
 806 |     "node_modules/@tailwindcss/oxide-freebsd-x64": {
 807 |       "version": "4.1.13",
 808 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-freebsd-x64/-/oxide-freebsd-x64-4.1.13.tgz",
 809 |       "integrity": "sha512-Wt8KvASHwSXhKE/dJLCCWcTSVmBj3xhVhp/aF3RpAhGeZ3sVo7+NTfgiN8Vey/Fi8prRClDs6/f0KXPDTZE6nQ==",
 810 |       "cpu": [
 811 |         "x64"
 812 |       ],
 813 |       "dev": true,
 814 |       "license": "MIT",
 815 |       "optional": true,
 816 |       "os": [
 817 |         "freebsd"
 818 |       ],
 819 |       "engines": {
 820 |         "node": ">= 10"
 821 |       }
 822 |     },
 823 |     "node_modules/@tailwindcss/oxide-linux-arm-gnueabihf": {
 824 |       "version": "4.1.13",
 825 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-linux-arm-gnueabihf/-/oxide-linux-arm-gnueabihf-4.1.13.tgz",
 826 |       "integrity": "sha512-mbVbcAsW3Gkm2MGwA93eLtWrwajz91aXZCNSkGTx/R5eb6KpKD5q8Ueckkh9YNboU8RH7jiv+ol/I7ZyQ9H7Bw==",
 827 |       "cpu": [
 828 |         "arm"
 829 |       ],
 830 |       "dev": true,
 831 |       "license": "MIT",
 832 |       "optional": true,
 833 |       "os": [
 834 |         "linux"
 835 |       ],
 836 |       "engines": {
 837 |         "node": ">= 10"
 838 |       }
 839 |     },
 840 |     "node_modules/@tailwindcss/oxide-linux-arm64-gnu": {
 841 |       "version": "4.1.13",
 842 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-linux-arm64-gnu/-/oxide-linux-arm64-gnu-4.1.13.tgz",
 843 |       "integrity": "sha512-wdtfkmpXiwej/yoAkrCP2DNzRXCALq9NVLgLELgLim1QpSfhQM5+ZxQQF8fkOiEpuNoKLp4nKZ6RC4kmeFH0HQ==",
 844 |       "cpu": [
 845 |         "arm64"
 846 |       ],
 847 |       "dev": true,
 848 |       "license": "MIT",
 849 |       "optional": true,
 850 |       "os": [
 851 |         "linux"
 852 |       ],
 853 |       "engines": {
 854 |         "node": ">= 10"
 855 |       }
 856 |     },
 857 |     "node_modules/@tailwindcss/oxide-linux-arm64-musl": {
 858 |       "version": "4.1.13",
 859 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-linux-arm64-musl/-/oxide-linux-arm64-musl-4.1.13.tgz",
 860 |       "integrity": "sha512-hZQrmtLdhyqzXHB7mkXfq0IYbxegaqTmfa1p9MBj72WPoDD3oNOh1Lnxf6xZLY9C3OV6qiCYkO1i/LrzEdW2mg==",
 861 |       "cpu": [
 862 |         "arm64"
 863 |       ],
 864 |       "dev": true,
 865 |       "license": "MIT",
 866 |       "optional": true,
 867 |       "os": [
 868 |         "linux"
 869 |       ],
 870 |       "engines": {
 871 |         "node": ">= 10"
 872 |       }
 873 |     },
 874 |     "node_modules/@tailwindcss/oxide-linux-x64-gnu": {
 875 |       "version": "4.1.13",
 876 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-linux-x64-gnu/-/oxide-linux-x64-gnu-4.1.13.tgz",
 877 |       "integrity": "sha512-uaZTYWxSXyMWDJZNY1Ul7XkJTCBRFZ5Fo6wtjrgBKzZLoJNrG+WderJwAjPzuNZOnmdrVg260DKwXCFtJ/hWRQ==",
 878 |       "cpu": [
 879 |         "x64"
 880 |       ],
 881 |       "dev": true,
 882 |       "license": "MIT",
 883 |       "optional": true,
 884 |       "os": [
 885 |         "linux"
 886 |       ],
 887 |       "engines": {
 888 |         "node": ">= 10"
 889 |       }
 890 |     },
 891 |     "node_modules/@tailwindcss/oxide-linux-x64-musl": {
 892 |       "version": "4.1.13",
 893 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-linux-x64-musl/-/oxide-linux-x64-musl-4.1.13.tgz",
 894 |       "integrity": "sha512-oXiPj5mi4Hdn50v5RdnuuIms0PVPI/EG4fxAfFiIKQh5TgQgX7oSuDWntHW7WNIi/yVLAiS+CRGW4RkoGSSgVQ==",
 895 |       "cpu": [
 896 |         "x64"
 897 |       ],
 898 |       "dev": true,
 899 |       "license": "MIT",
 900 |       "optional": true,
 901 |       "os": [
 902 |         "linux"
 903 |       ],
 904 |       "engines": {
 905 |         "node": ">= 10"
 906 |       }
 907 |     },
 908 |     "node_modules/@tailwindcss/oxide-wasm32-wasi": {
 909 |       "version": "4.1.13",
 910 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-wasm32-wasi/-/oxide-wasm32-wasi-4.1.13.tgz",
 911 |       "integrity": "sha512-+LC2nNtPovtrDwBc/nqnIKYh/W2+R69FA0hgoeOn64BdCX522u19ryLh3Vf3F8W49XBcMIxSe665kwy21FkhvA==",
 912 |       "bundleDependencies": [
 913 |         "@napi-rs/wasm-runtime",
 914 |         "@emnapi/core",
 915 |         "@emnapi/runtime",
 916 |         "@tybys/wasm-util",
 917 |         "@emnapi/wasi-threads",
 918 |         "tslib"
 919 |       ],
 920 |       "cpu": [
 921 |         "wasm32"
 922 |       ],
 923 |       "dev": true,
 924 |       "license": "MIT",
 925 |       "optional": true,
 926 |       "dependencies": {
 927 |         "@emnapi/core": "^1.4.5",
 928 |         "@emnapi/runtime": "^1.4.5",
 929 |         "@emnapi/wasi-threads": "^1.0.4",
 930 |         "@napi-rs/wasm-runtime": "^0.2.12",
 931 |         "@tybys/wasm-util": "^0.10.0",
 932 |         "tslib": "^2.8.0"
 933 |       },
 934 |       "engines": {
 935 |         "node": ">=14.0.0"
 936 |       }
 937 |     },
 938 |     "node_modules/@tailwindcss/oxide-win32-arm64-msvc": {
 939 |       "version": "4.1.13",
 940 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-win32-arm64-msvc/-/oxide-win32-arm64-msvc-4.1.13.tgz",
 941 |       "integrity": "sha512-dziTNeQXtoQ2KBXmrjCxsuPk3F3CQ/yb7ZNZNA+UkNTeiTGgfeh+gH5Pi7mRncVgcPD2xgHvkFCh/MhZWSgyQg==",
 942 |       "cpu": [
 943 |         "arm64"
 944 |       ],
 945 |       "dev": true,
 946 |       "license": "MIT",
 947 |       "optional": true,
 948 |       "os": [
 949 |         "win32"
 950 |       ],
 951 |       "engines": {
 952 |         "node": ">= 10"
 953 |       }
 954 |     },
 955 |     "node_modules/@tailwindcss/oxide-win32-x64-msvc": {
 956 |       "version": "4.1.13",
 957 |       "resolved": "https://registry.npmjs.org/@tailwindcss/oxide-win32-x64-msvc/-/oxide-win32-x64-msvc-4.1.13.tgz",
 958 |       "integrity": "sha512-3+LKesjXydTkHk5zXX01b5KMzLV1xl2mcktBJkje7rhFUpUlYJy7IMOLqjIRQncLTa1WZZiFY/foAeB5nmaiTw==",
 959 |       "cpu": [
 960 |         "x64"
 961 |       ],
 962 |       "dev": true,
 963 |       "license": "MIT",
 964 |       "optional": true,
 965 |       "os": [
 966 |         "win32"
 967 |       ],
 968 |       "engines": {
 969 |         "node": ">= 10"
 970 |       }
 971 |     },
 972 |     "node_modules/@tailwindcss/postcss": {
 973 |       "version": "4.1.13",
 974 |       "resolved": "https://registry.npmjs.org/@tailwindcss/postcss/-/postcss-4.1.13.tgz",
 975 |       "integrity": "sha512-HLgx6YSFKJT7rJqh9oJs/TkBFhxuMOfUKSBEPYwV+t78POOBsdQ7crhZLzwcH3T0UyUuOzU/GK5pk5eKr3wCiQ==",
 976 |       "dev": true,
 977 |       "license": "MIT",
 978 |       "dependencies": {
 979 |         "@alloc/quick-lru": "^5.2.0",
 980 |         "@tailwindcss/node": "4.1.13",
 981 |         "@tailwindcss/oxide": "4.1.13",
 982 |         "postcss": "^8.4.41",
 983 |         "tailwindcss": "4.1.13"
 984 |       }
 985 |     },
 986 |     "node_modules/@types/node": {
 987 |       "version": "20.19.13",
 988 |       "resolved": "https://registry.npmjs.org/@types/node/-/node-20.19.13.tgz",
 989 |       "integrity": "sha512-yCAeZl7a0DxgNVteXFHt9+uyFbqXGy/ShC4BlcHkoE0AfGXYv/BUiplV72DjMYXHDBXFjhvr6DD1NiRVfB4j8g==",
 990 |       "dev": true,
 991 |       "license": "MIT",
 992 |       "dependencies": {
 993 |         "undici-types": "~6.21.0"
 994 |       }
 995 |     },
 996 |     "node_modules/@types/react": {
 997 |       "version": "19.1.12",
 998 |       "resolved": "https://registry.npmjs.org/@types/react/-/react-19.1.12.tgz",
 999 |       "integrity": "sha512-cMoR+FoAf/Jyq6+Df2/Z41jISvGZZ2eTlnsaJRptmZ76Caldwy1odD4xTr/gNV9VLj0AWgg/nmkevIyUfIIq5w==",
1000 |       "devOptional": true,
1001 |       "license": "MIT",
1002 |       "dependencies": {
1003 |         "csstype": "^3.0.2"
1004 |       }
1005 |     },
1006 |     "node_modules/@types/react-dom": {
1007 |       "version": "19.1.9",
1008 |       "resolved": "https://registry.npmjs.org/@types/react-dom/-/react-dom-19.1.9.tgz",
1009 |       "integrity": "sha512-qXRuZaOsAdXKFyOhRBg6Lqqc0yay13vN7KrIg4L7N4aaHN68ma9OK3NE1BoDFgFOTfM7zg+3/8+2n8rLUH3OKQ==",
1010 |       "dev": true,
1011 |       "license": "MIT",
1012 |       "peerDependencies": {
1013 |         "@types/react": "^19.0.0"
1014 |       }
1015 |     },
1016 |     "node_modules/caniuse-lite": {
1017 |       "version": "1.0.30001739",
1018 |       "resolved": "https://registry.npmjs.org/caniuse-lite/-/caniuse-lite-1.0.30001739.tgz",
1019 |       "integrity": "sha512-y+j60d6ulelrNSwpPyrHdl+9mJnQzHBr08xm48Qno0nSk4h3Qojh+ziv2qE6rXf4k3tadF4o1J/1tAbVm1NtnA==",
1020 |       "funding": [
1021 |         {
1022 |           "type": "opencollective",
1023 |           "url": "https://opencollective.com/browserslist"
1024 |         },
1025 |         {
1026 |           "type": "tidelift",
1027 |           "url": "https://tidelift.com/funding/github/npm/caniuse-lite"
1028 |         },
1029 |         {
1030 |           "type": "github",
1031 |           "url": "https://github.com/sponsors/ai"
1032 |         }
1033 |       ],
1034 |       "license": "CC-BY-4.0"
1035 |     },
1036 |     "node_modules/chownr": {
1037 |       "version": "3.0.0",
1038 |       "resolved": "https://registry.npmjs.org/chownr/-/chownr-3.0.0.tgz",
1039 |       "integrity": "sha512-+IxzY9BZOQd/XuYPRmrvEVjF/nqj5kgT4kEq7VofrDoM1MxoRjEWkrCC3EtLi59TVawxTAn+orJwFQcrqEN1+g==",
1040 |       "dev": true,
1041 |       "license": "BlueOak-1.0.0",
1042 |       "engines": {
1043 |         "node": ">=18"
1044 |       }
1045 |     },
1046 |     "node_modules/class-variance-authority": {
1047 |       "version": "0.7.1",
1048 |       "resolved": "https://registry.npmjs.org/class-variance-authority/-/class-variance-authority-0.7.1.tgz",
1049 |       "integrity": "sha512-Ka+9Trutv7G8M6WT6SeiRWz792K5qEqIGEGzXKhAE6xOWAY6pPH8U+9IY3oCMv6kqTmLsv7Xh/2w2RigkePMsg==",
1050 |       "license": "Apache-2.0",
1051 |       "dependencies": {
1052 |         "clsx": "^2.1.1"
1053 |       },
1054 |       "funding": {
1055 |         "url": "https://polar.sh/cva"
1056 |       }
1057 |     },
1058 |     "node_modules/client-only": {
1059 |       "version": "0.0.1",
1060 |       "resolved": "https://registry.npmjs.org/client-only/-/client-only-0.0.1.tgz",
1061 |       "integrity": "sha512-IV3Ou0jSMzZrd3pZ48nLkT9DA7Ag1pnPzaiQhpW7c3RbcqqzvzzVu+L8gfqMp/8IM2MQtSiqaCxrrcfu8I8rMA==",
1062 |       "license": "MIT"
1063 |     },
1064 |     "node_modules/clsx": {
1065 |       "version": "2.1.1",
1066 |       "resolved": "https://registry.npmjs.org/clsx/-/clsx-2.1.1.tgz",
1067 |       "integrity": "sha512-eYm0QWBtUrBWZWG0d386OGAw16Z995PiOVo2B7bjWSbHedGl5e0ZWaq65kOGgUSNesEIDkB9ISbTg/JK9dhCZA==",
1068 |       "license": "MIT",
1069 |       "engines": {
1070 |         "node": ">=6"
1071 |       }
1072 |     },
1073 |     "node_modules/color": {
1074 |       "version": "4.2.3",
1075 |       "resolved": "https://registry.npmjs.org/color/-/color-4.2.3.tgz",
1076 |       "integrity": "sha512-1rXeuUUiGGrykh+CeBdu5Ie7OJwinCgQY0bc7GCRxy5xVHy+moaqkpL/jqQq0MtQOeYcrqEz4abc5f0KtU7W4A==",
1077 |       "license": "MIT",
1078 |       "optional": true,
1079 |       "dependencies": {
1080 |         "color-convert": "^2.0.1",
1081 |         "color-string": "^1.9.0"
1082 |       },
1083 |       "engines": {
1084 |         "node": ">=12.5.0"
1085 |       }
1086 |     },
1087 |     "node_modules/color-convert": {
1088 |       "version": "2.0.1",
1089 |       "resolved": "https://registry.npmjs.org/color-convert/-/color-convert-2.0.1.tgz",
1090 |       "integrity": "sha512-RRECPsj7iu/xb5oKYcsFHSppFNnsj/52OVTRKb4zP5onXwVF3zVmmToNcOfGC+CRDpfK/U584fMg38ZHCaElKQ==",
1091 |       "license": "MIT",
1092 |       "optional": true,
1093 |       "dependencies": {
1094 |         "color-name": "~1.1.4"
1095 |       },
1096 |       "engines": {
1097 |         "node": ">=7.0.0"
1098 |       }
1099 |     },
1100 |     "node_modules/color-name": {
1101 |       "version": "1.1.4",
1102 |       "resolved": "https://registry.npmjs.org/color-name/-/color-name-1.1.4.tgz",
1103 |       "integrity": "sha512-dOy+3AuW3a2wNbZHIuMZpTcgjGuLU/uBL/ubcZF9OXbDo8ff4O8yVp5Bf0efS8uEoYo5q4Fx7dY9OgQGXgAsQA==",
1104 |       "license": "MIT",
1105 |       "optional": true
1106 |     },
1107 |     "node_modules/color-string": {
1108 |       "version": "1.9.1",
1109 |       "resolved": "https://registry.npmjs.org/color-string/-/color-string-1.9.1.tgz",
1110 |       "integrity": "sha512-shrVawQFojnZv6xM40anx4CkoDP+fZsw/ZerEMsW/pyzsRbElpsL/DBVW7q3ExxwusdNXI3lXpuhEZkzs8p5Eg==",
1111 |       "license": "MIT",
1112 |       "optional": true,
1113 |       "dependencies": {
1114 |         "color-name": "^1.0.0",
1115 |         "simple-swizzle": "^0.2.2"
1116 |       }
1117 |     },
1118 |     "node_modules/csstype": {
1119 |       "version": "3.1.3",
1120 |       "resolved": "https://registry.npmjs.org/csstype/-/csstype-3.1.3.tgz",
1121 |       "integrity": "sha512-M1uQkMl8rQK/szD0LNhtqxIPLpimGm8sOBwU7lLnCpSbTyY3yeU1Vc7l4KT5zT4s/yOxHH5O7tIuuLOCnLADRw==",
1122 |       "devOptional": true,
1123 |       "license": "MIT"
1124 |     },
1125 |     "node_modules/detect-libc": {
1126 |       "version": "2.0.4",
1127 |       "resolved": "https://registry.npmjs.org/detect-libc/-/detect-libc-2.0.4.tgz",
1128 |       "integrity": "sha512-3UDv+G9CsCKO1WKMGw9fwq/SWJYbI0c5Y7LU1AXYoDdbhE2AHQ6N6Nb34sG8Fj7T5APy8qXDCKuuIHd1BR0tVA==",
1129 |       "devOptional": true,
1130 |       "license": "Apache-2.0",
1131 |       "engines": {
1132 |         "node": ">=8"
1133 |       }
1134 |     },
1135 |     "node_modules/enhanced-resolve": {
1136 |       "version": "5.18.3",
1137 |       "resolved": "https://registry.npmjs.org/enhanced-resolve/-/enhanced-resolve-5.18.3.tgz",
1138 |       "integrity": "sha512-d4lC8xfavMeBjzGr2vECC3fsGXziXZQyJxD868h2M/mBI3PwAuODxAkLkq5HYuvrPYcUtiLzsTo8U3PgX3Ocww==",
1139 |       "dev": true,
1140 |       "license": "MIT",
1141 |       "dependencies": {
1142 |         "graceful-fs": "^4.2.4",
1143 |         "tapable": "^2.2.0"
1144 |       },
1145 |       "engines": {
1146 |         "node": ">=10.13.0"
1147 |       }
1148 |     },
1149 |     "node_modules/graceful-fs": {
1150 |       "version": "4.2.11",
1151 |       "resolved": "https://registry.npmjs.org/graceful-fs/-/graceful-fs-4.2.11.tgz",
1152 |       "integrity": "sha512-RbJ5/jmFcNNCcDV5o9eTnBLJ/HszWV0P73bc+Ff4nS/rJj+YaS6IGyiOL0VoBYX+l1Wrl3k63h/KrH+nhJ0XvQ==",
1153 |       "dev": true,
1154 |       "license": "ISC"
1155 |     },
1156 |     "node_modules/is-arrayish": {
1157 |       "version": "0.3.2",
1158 |       "resolved": "https://registry.npmjs.org/is-arrayish/-/is-arrayish-0.3.2.tgz",
1159 |       "integrity": "sha512-eVRqCvVlZbuw3GrM63ovNSNAeA1K16kaR/LRY/92w0zxQ5/1YzwblUX652i4Xs9RwAGjW9d9y6X88t8OaAJfWQ==",
1160 |       "license": "MIT",
1161 |       "optional": true
1162 |     },
1163 |     "node_modules/jiti": {
1164 |       "version": "2.5.1",
1165 |       "resolved": "https://registry.npmjs.org/jiti/-/jiti-2.5.1.tgz",
1166 |       "integrity": "sha512-twQoecYPiVA5K/h6SxtORw/Bs3ar+mLUtoPSc7iMXzQzK8d7eJ/R09wmTwAjiamETn1cXYPGfNnu7DMoHgu12w==",
1167 |       "dev": true,
1168 |       "license": "MIT",
1169 |       "bin": {
1170 |         "jiti": "lib/jiti-cli.mjs"
1171 |       }
1172 |     },
1173 |     "node_modules/lightningcss": {
1174 |       "version": "1.30.1",
1175 |       "resolved": "https://registry.npmjs.org/lightningcss/-/lightningcss-1.30.1.tgz",
1176 |       "integrity": "sha512-xi6IyHML+c9+Q3W0S4fCQJOym42pyurFiJUHEcEyHS0CeKzia4yZDEsLlqOFykxOdHpNy0NmvVO31vcSqAxJCg==",
1177 |       "dev": true,
1178 |       "license": "MPL-2.0",
1179 |       "dependencies": {
1180 |         "detect-libc": "^2.0.3"
1181 |       },
1182 |       "engines": {
1183 |         "node": ">= 12.0.0"
1184 |       },
1185 |       "funding": {
1186 |         "type": "opencollective",
1187 |         "url": "https://opencollective.com/parcel"
1188 |       },
1189 |       "optionalDependencies": {
1190 |         "lightningcss-darwin-arm64": "1.30.1",
1191 |         "lightningcss-darwin-x64": "1.30.1",
1192 |         "lightningcss-freebsd-x64": "1.30.1",
1193 |         "lightningcss-linux-arm-gnueabihf": "1.30.1",
1194 |         "lightningcss-linux-arm64-gnu": "1.30.1",
1195 |         "lightningcss-linux-arm64-musl": "1.30.1",
1196 |         "lightningcss-linux-x64-gnu": "1.30.1",
1197 |         "lightningcss-linux-x64-musl": "1.30.1",
1198 |         "lightningcss-win32-arm64-msvc": "1.30.1",
1199 |         "lightningcss-win32-x64-msvc": "1.30.1"
1200 |       }
1201 |     },
1202 |     "node_modules/lightningcss-darwin-arm64": {
1203 |       "version": "1.30.1",
1204 |       "resolved": "https://registry.npmjs.org/lightningcss-darwin-arm64/-/lightningcss-darwin-arm64-1.30.1.tgz",
1205 |       "integrity": "sha512-c8JK7hyE65X1MHMN+Viq9n11RRC7hgin3HhYKhrMyaXflk5GVplZ60IxyoVtzILeKr+xAJwg6zK6sjTBJ0FKYQ==",
1206 |       "cpu": [
1207 |         "arm64"
1208 |       ],
1209 |       "dev": true,
1210 |       "license": "MPL-2.0",
1211 |       "optional": true,
1212 |       "os": [
1213 |         "darwin"
1214 |       ],
1215 |       "engines": {
1216 |         "node": ">= 12.0.0"
1217 |       },
1218 |       "funding": {
1219 |         "type": "opencollective",
1220 |         "url": "https://opencollective.com/parcel"
1221 |       }
1222 |     },
1223 |     "node_modules/lightningcss-darwin-x64": {
1224 |       "version": "1.30.1",
1225 |       "resolved": "https://registry.npmjs.org/lightningcss-darwin-x64/-/lightningcss-darwin-x64-1.30.1.tgz",
1226 |       "integrity": "sha512-k1EvjakfumAQoTfcXUcHQZhSpLlkAuEkdMBsI/ivWw9hL+7FtilQc0Cy3hrx0AAQrVtQAbMI7YjCgYgvn37PzA==",
1227 |       "cpu": [
1228 |         "x64"
1229 |       ],
1230 |       "dev": true,
1231 |       "license": "MPL-2.0",
1232 |       "optional": true,
1233 |       "os": [
1234 |         "darwin"
1235 |       ],
1236 |       "engines": {
1237 |         "node": ">= 12.0.0"
1238 |       },
1239 |       "funding": {
1240 |         "type": "opencollective",
1241 |         "url": "https://opencollective.com/parcel"
1242 |       }
1243 |     },
1244 |     "node_modules/lightningcss-freebsd-x64": {
1245 |       "version": "1.30.1",
1246 |       "resolved": "https://registry.npmjs.org/lightningcss-freebsd-x64/-/lightningcss-freebsd-x64-1.30.1.tgz",
1247 |       "integrity": "sha512-kmW6UGCGg2PcyUE59K5r0kWfKPAVy4SltVeut+umLCFoJ53RdCUWxcRDzO1eTaxf/7Q2H7LTquFHPL5R+Gjyig==",
1248 |       "cpu": [
1249 |         "x64"
1250 |       ],
1251 |       "dev": true,
1252 |       "license": "MPL-2.0",
1253 |       "optional": true,
1254 |       "os": [
1255 |         "freebsd"
1256 |       ],
1257 |       "engines": {
1258 |         "node": ">= 12.0.0"
1259 |       },
1260 |       "funding": {
1261 |         "type": "opencollective",
1262 |         "url": "https://opencollective.com/parcel"
1263 |       }
1264 |     },
1265 |     "node_modules/lightningcss-linux-arm-gnueabihf": {
1266 |       "version": "1.30.1",
1267 |       "resolved": "https://registry.npmjs.org/lightningcss-linux-arm-gnueabihf/-/lightningcss-linux-arm-gnueabihf-1.30.1.tgz",
1268 |       "integrity": "sha512-MjxUShl1v8pit+6D/zSPq9S9dQ2NPFSQwGvxBCYaBYLPlCWuPh9/t1MRS8iUaR8i+a6w7aps+B4N0S1TYP/R+Q==",
1269 |       "cpu": [
1270 |         "arm"
1271 |       ],
1272 |       "dev": true,
1273 |       "license": "MPL-2.0",
1274 |       "optional": true,
1275 |       "os": [
1276 |         "linux"
1277 |       ],
1278 |       "engines": {
1279 |         "node": ">= 12.0.0"
1280 |       },
1281 |       "funding": {
1282 |         "type": "opencollective",
1283 |         "url": "https://opencollective.com/parcel"
1284 |       }
1285 |     },
1286 |     "node_modules/lightningcss-linux-arm64-gnu": {
1287 |       "version": "1.30.1",
1288 |       "resolved": "https://registry.npmjs.org/lightningcss-linux-arm64-gnu/-/lightningcss-linux-arm64-gnu-1.30.1.tgz",
1289 |       "integrity": "sha512-gB72maP8rmrKsnKYy8XUuXi/4OctJiuQjcuqWNlJQ6jZiWqtPvqFziskH3hnajfvKB27ynbVCucKSm2rkQp4Bw==",
1290 |       "cpu": [
1291 |         "arm64"
1292 |       ],
1293 |       "dev": true,
1294 |       "license": "MPL-2.0",
1295 |       "optional": true,
1296 |       "os": [
1297 |         "linux"
1298 |       ],
1299 |       "engines": {
1300 |         "node": ">= 12.0.0"
1301 |       },
1302 |       "funding": {
1303 |         "type": "opencollective",
1304 |         "url": "https://opencollective.com/parcel"
1305 |       }
1306 |     },
1307 |     "node_modules/lightningcss-linux-arm64-musl": {
1308 |       "version": "1.30.1",
1309 |       "resolved": "https://registry.npmjs.org/lightningcss-linux-arm64-musl/-/lightningcss-linux-arm64-musl-1.30.1.tgz",
1310 |       "integrity": "sha512-jmUQVx4331m6LIX+0wUhBbmMX7TCfjF5FoOH6SD1CttzuYlGNVpA7QnrmLxrsub43ClTINfGSYyHe2HWeLl5CQ==",
1311 |       "cpu": [
1312 |         "arm64"
1313 |       ],
1314 |       "dev": true,
1315 |       "license": "MPL-2.0",
1316 |       "optional": true,
1317 |       "os": [
1318 |         "linux"
1319 |       ],
1320 |       "engines": {
1321 |         "node": ">= 12.0.0"
1322 |       },
1323 |       "funding": {
1324 |         "type": "opencollective",
1325 |         "url": "https://opencollective.com/parcel"
1326 |       }
1327 |     },
1328 |     "node_modules/lightningcss-linux-x64-gnu": {
1329 |       "version": "1.30.1",
1330 |       "resolved": "https://registry.npmjs.org/lightningcss-linux-x64-gnu/-/lightningcss-linux-x64-gnu-1.30.1.tgz",
1331 |       "integrity": "sha512-piWx3z4wN8J8z3+O5kO74+yr6ze/dKmPnI7vLqfSqI8bccaTGY5xiSGVIJBDd5K5BHlvVLpUB3S2YCfelyJ1bw==",
1332 |       "cpu": [
1333 |         "x64"
1334 |       ],
1335 |       "dev": true,
1336 |       "license": "MPL-2.0",
1337 |       "optional": true,
1338 |       "os": [
1339 |         "linux"
1340 |       ],
1341 |       "engines": {
1342 |         "node": ">= 12.0.0"
1343 |       },
1344 |       "funding": {
1345 |         "type": "opencollective",
1346 |         "url": "https://opencollective.com/parcel"
1347 |       }
1348 |     },
1349 |     "node_modules/lightningcss-linux-x64-musl": {
1350 |       "version": "1.30.1",
1351 |       "resolved": "https://registry.npmjs.org/lightningcss-linux-x64-musl/-/lightningcss-linux-x64-musl-1.30.1.tgz",
1352 |       "integrity": "sha512-rRomAK7eIkL+tHY0YPxbc5Dra2gXlI63HL+v1Pdi1a3sC+tJTcFrHX+E86sulgAXeI7rSzDYhPSeHHjqFhqfeQ==",
1353 |       "cpu": [
1354 |         "x64"
1355 |       ],
1356 |       "dev": true,
1357 |       "license": "MPL-2.0",
1358 |       "optional": true,
1359 |       "os": [
1360 |         "linux"
1361 |       ],
1362 |       "engines": {
1363 |         "node": ">= 12.0.0"
1364 |       },
1365 |       "funding": {
1366 |         "type": "opencollective",
1367 |         "url": "https://opencollective.com/parcel"
1368 |       }
1369 |     },
1370 |     "node_modules/lightningcss-win32-arm64-msvc": {
1371 |       "version": "1.30.1",
1372 |       "resolved": "https://registry.npmjs.org/lightningcss-win32-arm64-msvc/-/lightningcss-win32-arm64-msvc-1.30.1.tgz",
1373 |       "integrity": "sha512-mSL4rqPi4iXq5YVqzSsJgMVFENoa4nGTT/GjO2c0Yl9OuQfPsIfncvLrEW6RbbB24WtZ3xP/2CCmI3tNkNV4oA==",
1374 |       "cpu": [
1375 |         "arm64"
1376 |       ],
1377 |       "dev": true,
1378 |       "license": "MPL-2.0",
1379 |       "optional": true,
1380 |       "os": [
1381 |         "win32"
1382 |       ],
1383 |       "engines": {
1384 |         "node": ">= 12.0.0"
1385 |       },
1386 |       "funding": {
1387 |         "type": "opencollective",
1388 |         "url": "https://opencollective.com/parcel"
1389 |       }
1390 |     },
1391 |     "node_modules/lightningcss-win32-x64-msvc": {
1392 |       "version": "1.30.1",
1393 |       "resolved": "https://registry.npmjs.org/lightningcss-win32-x64-msvc/-/lightningcss-win32-x64-msvc-1.30.1.tgz",
1394 |       "integrity": "sha512-PVqXh48wh4T53F/1CCu8PIPCxLzWyCnn/9T5W1Jpmdy5h9Cwd+0YQS6/LwhHXSafuc61/xg9Lv5OrCby6a++jg==",
1395 |       "cpu": [
1396 |         "x64"
1397 |       ],
1398 |       "dev": true,
1399 |       "license": "MPL-2.0",
1400 |       "optional": true,
1401 |       "os": [
1402 |         "win32"
1403 |       ],
1404 |       "engines": {
1405 |         "node": ">= 12.0.0"
1406 |       },
1407 |       "funding": {
1408 |         "type": "opencollective",
1409 |         "url": "https://opencollective.com/parcel"
1410 |       }
1411 |     },
1412 |     "node_modules/lucide-react": {
1413 |       "version": "0.525.0",
1414 |       "resolved": "https://registry.npmjs.org/lucide-react/-/lucide-react-0.525.0.tgz",
1415 |       "integrity": "sha512-Tm1txJ2OkymCGkvwoHt33Y2JpN5xucVq1slHcgE6Lk0WjDfjgKWor5CdVER8U6DvcfMwh4M8XxmpTiyzfmfDYQ==",
1416 |       "license": "ISC",
1417 |       "peerDependencies": {
1418 |         "react": "^16.5.1 || ^17.0.0 || ^18.0.0 || ^19.0.0"
1419 |       }
1420 |     },
1421 |     "node_modules/magic-string": {
1422 |       "version": "0.30.18",
1423 |       "resolved": "https://registry.npmjs.org/magic-string/-/magic-string-0.30.18.tgz",
1424 |       "integrity": "sha512-yi8swmWbO17qHhwIBNeeZxTceJMeBvWJaId6dyvTSOwTipqeHhMhOrz6513r1sOKnpvQ7zkhlG8tPrpilwTxHQ==",
1425 |       "dev": true,
1426 |       "license": "MIT",
1427 |       "dependencies": {
1428 |         "@jridgewell/sourcemap-codec": "^1.5.5"
1429 |       }
1430 |     },
1431 |     "node_modules/minipass": {
1432 |       "version": "7.1.2",
1433 |       "resolved": "https://registry.npmjs.org/minipass/-/minipass-7.1.2.tgz",
1434 |       "integrity": "sha512-qOOzS1cBTWYF4BH8fVePDBOO9iptMnGUEZwNc/cMWnTV2nVLZ7VoNWEPHkYczZA0pdoA7dl6e7FL659nX9S2aw==",
1435 |       "dev": true,
1436 |       "license": "ISC",
1437 |       "engines": {
1438 |         "node": ">=16 || 14 >=14.17"
1439 |       }
1440 |     },
1441 |     "node_modules/minizlib": {
1442 |       "version": "3.0.2",
1443 |       "resolved": "https://registry.npmjs.org/minizlib/-/minizlib-3.0.2.tgz",
1444 |       "integrity": "sha512-oG62iEk+CYt5Xj2YqI5Xi9xWUeZhDI8jjQmC5oThVH5JGCTgIjr7ciJDzC7MBzYd//WvR1OTmP5Q38Q8ShQtVA==",
1445 |       "dev": true,
1446 |       "license": "MIT",
1447 |       "dependencies": {
1448 |         "minipass": "^7.1.2"
1449 |       },
1450 |       "engines": {
1451 |         "node": ">= 18"
1452 |       }
1453 |     },
1454 |     "node_modules/mkdirp": {
1455 |       "version": "3.0.1",
1456 |       "resolved": "https://registry.npmjs.org/mkdirp/-/mkdirp-3.0.1.tgz",
1457 |       "integrity": "sha512-+NsyUUAZDmo6YVHzL/stxSu3t9YS1iljliy3BSDrXJ/dkn1KYdmtZODGGjLcc9XLgVVpH4KshHB8XmZgMhaBXg==",
1458 |       "dev": true,
1459 |       "license": "MIT",
1460 |       "bin": {
1461 |         "mkdirp": "dist/cjs/src/bin.js"
1462 |       },
1463 |       "engines": {
1464 |         "node": ">=10"
1465 |       },
1466 |       "funding": {
1467 |         "url": "https://github.com/sponsors/isaacs"
1468 |       }
1469 |     },
1470 |     "node_modules/nanoid": {
1471 |       "version": "3.3.11",
1472 |       "resolved": "https://registry.npmjs.org/nanoid/-/nanoid-3.3.11.tgz",
1473 |       "integrity": "sha512-N8SpfPUnUp1bK+PMYW8qSWdl9U+wwNWI4QKxOYDy9JAro3WMX7p2OeVRF9v+347pnakNevPmiHhNmZ2HbFA76w==",
1474 |       "funding": [
1475 |         {
1476 |           "type": "github",
1477 |           "url": "https://github.com/sponsors/ai"
1478 |         }
1479 |       ],
1480 |       "license": "MIT",
1481 |       "bin": {
1482 |         "nanoid": "bin/nanoid.cjs"
1483 |       },
1484 |       "engines": {
1485 |         "node": "^10 || ^12 || ^13.7 || ^14 || >=15.0.1"
1486 |       }
1487 |     },
1488 |     "node_modules/next": {
1489 |       "version": "15.5.2",
1490 |       "resolved": "https://registry.npmjs.org/next/-/next-15.5.2.tgz",
1491 |       "integrity": "sha512-H8Otr7abj1glFhbGnvUt3gz++0AF1+QoCXEBmd/6aKbfdFwrn0LpA836Ed5+00va/7HQSDD+mOoVhn3tNy3e/Q==",
1492 |       "license": "MIT",
1493 |       "dependencies": {
1494 |         "@next/env": "15.5.2",
1495 |         "@swc/helpers": "0.5.15",
1496 |         "caniuse-lite": "^1.0.30001579",
1497 |         "postcss": "8.4.31",
1498 |         "styled-jsx": "5.1.6"
1499 |       },
1500 |       "bin": {
1501 |         "next": "dist/bin/next"
1502 |       },
1503 |       "engines": {
1504 |         "node": "^18.18.0 || ^19.8.0 || >= 20.0.0"
1505 |       },
1506 |       "optionalDependencies": {
1507 |         "@next/swc-darwin-arm64": "15.5.2",
1508 |         "@next/swc-darwin-x64": "15.5.2",
1509 |         "@next/swc-linux-arm64-gnu": "15.5.2",
1510 |         "@next/swc-linux-arm64-musl": "15.5.2",
1511 |         "@next/swc-linux-x64-gnu": "15.5.2",
1512 |         "@next/swc-linux-x64-musl": "15.5.2",
1513 |         "@next/swc-win32-arm64-msvc": "15.5.2",
1514 |         "@next/swc-win32-x64-msvc": "15.5.2",
1515 |         "sharp": "^0.34.3"
1516 |       },
1517 |       "peerDependencies": {
1518 |         "@opentelemetry/api": "^1.1.0",
1519 |         "@playwright/test": "^1.51.1",
1520 |         "babel-plugin-react-compiler": "*",
1521 |         "react": "^18.2.0 || 19.0.0-rc-de68d2f4-20241204 || ^19.0.0",
1522 |         "react-dom": "^18.2.0 || 19.0.0-rc-de68d2f4-20241204 || ^19.0.0",
1523 |         "sass": "^1.3.0"
1524 |       },
1525 |       "peerDependenciesMeta": {
1526 |         "@opentelemetry/api": {
1527 |           "optional": true
1528 |         },
1529 |         "@playwright/test": {
1530 |           "optional": true
1531 |         },
1532 |         "babel-plugin-react-compiler": {
1533 |           "optional": true
1534 |         },
1535 |         "sass": {
1536 |           "optional": true
1537 |         }
1538 |       }
1539 |     },
1540 |     "node_modules/next/node_modules/postcss": {
1541 |       "version": "8.4.31",
1542 |       "resolved": "https://registry.npmjs.org/postcss/-/postcss-8.4.31.tgz",
1543 |       "integrity": "sha512-PS08Iboia9mts/2ygV3eLpY5ghnUcfLV/EXTOW1E2qYxJKGGBUtNjN76FYHnMs36RmARn41bC0AZmn+rR0OVpQ==",
1544 |       "funding": [
1545 |         {
1546 |           "type": "opencollective",
1547 |           "url": "https://opencollective.com/postcss/"
1548 |         },
1549 |         {
1550 |           "type": "tidelift",
1551 |           "url": "https://tidelift.com/funding/github/npm/postcss"
1552 |         },
1553 |         {
1554 |           "type": "github",
1555 |           "url": "https://github.com/sponsors/ai"
1556 |         }
1557 |       ],
1558 |       "license": "MIT",
1559 |       "dependencies": {
1560 |         "nanoid": "^3.3.6",
1561 |         "picocolors": "^1.0.0",
1562 |         "source-map-js": "^1.0.2"
1563 |       },
1564 |       "engines": {
1565 |         "node": "^10 || ^12 || >=14"
1566 |       }
1567 |     },
1568 |     "node_modules/picocolors": {
1569 |       "version": "1.1.1",
1570 |       "resolved": "https://registry.npmjs.org/picocolors/-/picocolors-1.1.1.tgz",
1571 |       "integrity": "sha512-xceH2snhtb5M9liqDsmEw56le376mTZkEX/jEb/RxNFyegNul7eNslCXP9FDj/Lcu0X8KEyMceP2ntpaHrDEVA==",
1572 |       "license": "ISC"
1573 |     },
1574 |     "node_modules/postcss": {
1575 |       "version": "8.5.6",
1576 |       "resolved": "https://registry.npmjs.org/postcss/-/postcss-8.5.6.tgz",
1577 |       "integrity": "sha512-3Ybi1tAuwAP9s0r1UQ2J4n5Y0G05bJkpUIO0/bI9MhwmD70S5aTWbXGBwxHrelT+XM1k6dM0pk+SwNkpTRN7Pg==",
1578 |       "dev": true,
1579 |       "funding": [
1580 |         {
1581 |           "type": "opencollective",
1582 |           "url": "https://opencollective.com/postcss/"
1583 |         },
1584 |         {
1585 |           "type": "tidelift",
1586 |           "url": "https://tidelift.com/funding/github/npm/postcss"
1587 |         },
1588 |         {
1589 |           "type": "github",
1590 |           "url": "https://github.com/sponsors/ai"
1591 |         }
1592 |       ],
1593 |       "license": "MIT",
1594 |       "dependencies": {
1595 |         "nanoid": "^3.3.11",
1596 |         "picocolors": "^1.1.1",
1597 |         "source-map-js": "^1.2.1"
1598 |       },
1599 |       "engines": {
1600 |         "node": "^10 || ^12 || >=14"
1601 |       }
1602 |     },
1603 |     "node_modules/react": {
1604 |       "version": "19.1.1",
1605 |       "resolved": "https://registry.npmjs.org/react/-/react-19.1.1.tgz",
1606 |       "integrity": "sha512-w8nqGImo45dmMIfljjMwOGtbmC/mk4CMYhWIicdSflH91J9TyCyczcPFXJzrZ/ZXcgGRFeP6BU0BEJTw6tZdfQ==",
1607 |       "license": "MIT",
1608 |       "engines": {
1609 |         "node": ">=0.10.0"
1610 |       }
1611 |     },
1612 |     "node_modules/react-dom": {
1613 |       "version": "19.1.1",
1614 |       "resolved": "https://registry.npmjs.org/react-dom/-/react-dom-19.1.1.tgz",
1615 |       "integrity": "sha512-Dlq/5LAZgF0Gaz6yiqZCf6VCcZs1ghAJyrsu84Q/GT0gV+mCxbfmKNoGRKBYMJ8IEdGPqu49YWXD02GCknEDkw==",
1616 |       "license": "MIT",
1617 |       "dependencies": {
1618 |         "scheduler": "^0.26.0"
1619 |       },
1620 |       "peerDependencies": {
1621 |         "react": "^19.1.1"
1622 |       }
1623 |     },
1624 |     "node_modules/scheduler": {
1625 |       "version": "0.26.0",
1626 |       "resolved": "https://registry.npmjs.org/scheduler/-/scheduler-0.26.0.tgz",
1627 |       "integrity": "sha512-NlHwttCI/l5gCPR3D1nNXtWABUmBwvZpEQiD4IXSbIDq8BzLIK/7Ir5gTFSGZDUu37K5cMNp0hFtzO38sC7gWA==",
1628 |       "license": "MIT"
1629 |     },
1630 |     "node_modules/semver": {
1631 |       "version": "7.7.2",
1632 |       "resolved": "https://registry.npmjs.org/semver/-/semver-7.7.2.tgz",
1633 |       "integrity": "sha512-RF0Fw+rO5AMf9MAyaRXI4AV0Ulj5lMHqVxxdSgiVbixSCXoEmmX/jk0CuJw4+3SqroYO9VoUh+HcuJivvtJemA==",
1634 |       "license": "ISC",
1635 |       "optional": true,
1636 |       "bin": {
1637 |         "semver": "bin/semver.js"
1638 |       },
1639 |       "engines": {
1640 |         "node": ">=10"
1641 |       }
1642 |     },
1643 |     "node_modules/sharp": {
1644 |       "version": "0.34.3",
1645 |       "resolved": "https://registry.npmjs.org/sharp/-/sharp-0.34.3.tgz",
1646 |       "integrity": "sha512-eX2IQ6nFohW4DbvHIOLRB3MHFpYqaqvXd3Tp5e/T/dSH83fxaNJQRvDMhASmkNTsNTVF2/OOopzRCt7xokgPfg==",
1647 |       "hasInstallScript": true,
1648 |       "license": "Apache-2.0",
1649 |       "optional": true,
1650 |       "dependencies": {
1651 |         "color": "^4.2.3",
1652 |         "detect-libc": "^2.0.4",
1653 |         "semver": "^7.7.2"
1654 |       },
1655 |       "engines": {
1656 |         "node": "^18.17.0 || ^20.3.0 || >=21.0.0"
1657 |       },
1658 |       "funding": {
1659 |         "url": "https://opencollective.com/libvips"
1660 |       },
1661 |       "optionalDependencies": {
1662 |         "@img/sharp-darwin-arm64": "0.34.3",
1663 |         "@img/sharp-darwin-x64": "0.34.3",
1664 |         "@img/sharp-libvips-darwin-arm64": "1.2.0",
1665 |         "@img/sharp-libvips-darwin-x64": "1.2.0",
1666 |         "@img/sharp-libvips-linux-arm": "1.2.0",
1667 |         "@img/sharp-libvips-linux-arm64": "1.2.0",
1668 |         "@img/sharp-libvips-linux-ppc64": "1.2.0",
1669 |         "@img/sharp-libvips-linux-s390x": "1.2.0",
1670 |         "@img/sharp-libvips-linux-x64": "1.2.0",
1671 |         "@img/sharp-libvips-linuxmusl-arm64": "1.2.0",
1672 |         "@img/sharp-libvips-linuxmusl-x64": "1.2.0",
1673 |         "@img/sharp-linux-arm": "0.34.3",
1674 |         "@img/sharp-linux-arm64": "0.34.3",
1675 |         "@img/sharp-linux-ppc64": "0.34.3",
1676 |         "@img/sharp-linux-s390x": "0.34.3",
1677 |         "@img/sharp-linux-x64": "0.34.3",
1678 |         "@img/sharp-linuxmusl-arm64": "0.34.3",
1679 |         "@img/sharp-linuxmusl-x64": "0.34.3",
1680 |         "@img/sharp-wasm32": "0.34.3",
1681 |         "@img/sharp-win32-arm64": "0.34.3",
1682 |         "@img/sharp-win32-ia32": "0.34.3",
1683 |         "@img/sharp-win32-x64": "0.34.3"
1684 |       }
1685 |     },
1686 |     "node_modules/simple-swizzle": {
1687 |       "version": "0.2.2",
1688 |       "resolved": "https://registry.npmjs.org/simple-swizzle/-/simple-swizzle-0.2.2.tgz",
1689 |       "integrity": "sha512-JA//kQgZtbuY83m+xT+tXJkmJncGMTFT+C+g2h2R9uxkYIrE2yy9sgmcLhCnw57/WSD+Eh3J97FPEDFnbXnDUg==",
1690 |       "license": "MIT",
1691 |       "optional": true,
1692 |       "dependencies": {
1693 |         "is-arrayish": "^0.3.1"
1694 |       }
1695 |     },
1696 |     "node_modules/source-map-js": {
1697 |       "version": "1.2.1",
1698 |       "resolved": "https://registry.npmjs.org/source-map-js/-/source-map-js-1.2.1.tgz",
1699 |       "integrity": "sha512-UXWMKhLOwVKb728IUtQPXxfYU+usdybtUrK/8uGE8CQMvrhOpwvzDBwj0QhSL7MQc7vIsISBG8VQ8+IDQxpfQA==",
1700 |       "license": "BSD-3-Clause",
1701 |       "engines": {
1702 |         "node": ">=0.10.0"
1703 |       }
1704 |     },
1705 |     "node_modules/styled-jsx": {
1706 |       "version": "5.1.6",
1707 |       "resolved": "https://registry.npmjs.org/styled-jsx/-/styled-jsx-5.1.6.tgz",
1708 |       "integrity": "sha512-qSVyDTeMotdvQYoHWLNGwRFJHC+i+ZvdBRYosOFgC+Wg1vx4frN2/RG/NA7SYqqvKNLf39P2LSRA2pu6n0XYZA==",
1709 |       "license": "MIT",
1710 |       "dependencies": {
1711 |         "client-only": "0.0.1"
1712 |       },
1713 |       "engines": {
1714 |         "node": ">= 12.0.0"
1715 |       },
1716 |       "peerDependencies": {
1717 |         "react": ">= 16.8.0 || 17.x.x || ^18.0.0-0 || ^19.0.0-0"
1718 |       },
1719 |       "peerDependenciesMeta": {
1720 |         "@babel/core": {
1721 |           "optional": true
1722 |         },
1723 |         "babel-plugin-macros": {
1724 |           "optional": true
1725 |         }
1726 |       }
1727 |     },
1728 |     "node_modules/tailwind-merge": {
1729 |       "version": "3.3.1",
1730 |       "resolved": "https://registry.npmjs.org/tailwind-merge/-/tailwind-merge-3.3.1.tgz",
1731 |       "integrity": "sha512-gBXpgUm/3rp1lMZZrM/w7D8GKqshif0zAymAhbCyIt8KMe+0v9DQ7cdYLR4FHH/cKpdTXb+A/tKKU3eolfsI+g==",
1732 |       "license": "MIT",
1733 |       "funding": {
1734 |         "type": "github",
1735 |         "url": "https://github.com/sponsors/dcastil"
1736 |       }
1737 |     },
1738 |     "node_modules/tailwindcss": {
1739 |       "version": "4.1.13",
1740 |       "resolved": "https://registry.npmjs.org/tailwindcss/-/tailwindcss-4.1.13.tgz",
1741 |       "integrity": "sha512-i+zidfmTqtwquj4hMEwdjshYYgMbOrPzb9a0M3ZgNa0JMoZeFC6bxZvO8yr8ozS6ix2SDz0+mvryPeBs2TFE+w==",
1742 |       "dev": true,
1743 |       "license": "MIT"
1744 |     },
1745 |     "node_modules/tapable": {
1746 |       "version": "2.2.3",
1747 |       "resolved": "https://registry.npmjs.org/tapable/-/tapable-2.2.3.tgz",
1748 |       "integrity": "sha512-ZL6DDuAlRlLGghwcfmSn9sK3Hr6ArtyudlSAiCqQ6IfE+b+HHbydbYDIG15IfS5do+7XQQBdBiubF/cV2dnDzg==",
1749 |       "dev": true,
1750 |       "license": "MIT",
1751 |       "engines": {
1752 |         "node": ">=6"
1753 |       },
1754 |       "funding": {
1755 |         "type": "opencollective",
1756 |         "url": "https://opencollective.com/webpack"
1757 |       }
1758 |     },
1759 |     "node_modules/tar": {
1760 |       "version": "7.4.3",
1761 |       "resolved": "https://registry.npmjs.org/tar/-/tar-7.4.3.tgz",
1762 |       "integrity": "sha512-5S7Va8hKfV7W5U6g3aYxXmlPoZVAwUMy9AOKyF2fVuZa2UD3qZjg578OrLRt8PcNN1PleVaL/5/yYATNL0ICUw==",
1763 |       "dev": true,
1764 |       "license": "ISC",
1765 |       "dependencies": {
1766 |         "@isaacs/fs-minipass": "^4.0.0",
1767 |         "chownr": "^3.0.0",
1768 |         "minipass": "^7.1.2",
1769 |         "minizlib": "^3.0.1",
1770 |         "mkdirp": "^3.0.1",
1771 |         "yallist": "^5.0.0"
1772 |       },
1773 |       "engines": {
1774 |         "node": ">=18"
1775 |       }
1776 |     },
1777 |     "node_modules/tslib": {
1778 |       "version": "2.8.1",
1779 |       "resolved": "https://registry.npmjs.org/tslib/-/tslib-2.8.1.tgz",
1780 |       "integrity": "sha512-oJFu94HQb+KVduSUQL7wnpmqnfmLsOA/nAh6b6EH0wCEoK0/mPeXU6c3wKDV83MkOuHPRHtSXKKU99IBazS/2w==",
1781 |       "license": "0BSD"
1782 |     },
1783 |     "node_modules/tw-animate-css": {
1784 |       "version": "1.3.8",
1785 |       "resolved": "https://registry.npmjs.org/tw-animate-css/-/tw-animate-css-1.3.8.tgz",
1786 |       "integrity": "sha512-Qrk3PZ7l7wUcGYhwZloqfkWCmaXZAoqjkdbIDvzfGshwGtexa/DAs9koXxIkrpEasyevandomzCBAV1Yyop5rw==",
1787 |       "dev": true,
1788 |       "license": "MIT",
1789 |       "funding": {
1790 |         "url": "https://github.com/sponsors/Wombosvideo"
1791 |       }
1792 |     },
1793 |     "node_modules/typescript": {
1794 |       "version": "5.9.2",
1795 |       "resolved": "https://registry.npmjs.org/typescript/-/typescript-5.9.2.tgz",
1796 |       "integrity": "sha512-CWBzXQrc/qOkhidw1OzBTQuYRbfyxDXJMVJ1XNwUHGROVmuaeiEm3OslpZ1RV96d7SKKjZKrSJu3+t/xlw3R9A==",
1797 |       "dev": true,
1798 |       "license": "Apache-2.0",
1799 |       "bin": {
1800 |         "tsc": "bin/tsc",
1801 |         "tsserver": "bin/tsserver"
1802 |       },
1803 |       "engines": {
1804 |         "node": ">=14.17"
1805 |       }
1806 |     },
1807 |     "node_modules/undici-types": {
1808 |       "version": "6.21.0",
1809 |       "resolved": "https://registry.npmjs.org/undici-types/-/undici-types-6.21.0.tgz",
1810 |       "integrity": "sha512-iwDZqg0QAGrg9Rav5H4n0M64c3mkR59cJ6wQp+7C4nI0gsmExaedaYLNO44eT4AtBBwjbTiGPMlt2Md0T9H9JQ==",
1811 |       "dev": true,
1812 |       "license": "MIT"
1813 |     },
1814 |     "node_modules/yallist": {
1815 |       "version": "5.0.0",
1816 |       "resolved": "https://registry.npmjs.org/yallist/-/yallist-5.0.0.tgz",
1817 |       "integrity": "sha512-YgvUTfwqyc7UXVMrB+SImsVYSmTS8X/tSrtdNZMImM+n7+QTriRXyXim0mBrTXNeqzVF0KWGgHPeiyViFFrNDw==",
1818 |       "dev": true,
1819 |       "license": "BlueOak-1.0.0",
1820 |       "engines": {
1821 |         "node": ">=18"
1822 |       }
1823 |     }
1824 |   }
1825 | }
1826 | 


--------------------------------------------------------------------------------
/package.json:
--------------------------------------------------------------------------------
 1 | {
 2 |   "name": "nextjs-starters",
 3 |   "version": "0.1.0",
 4 |   "private": true,
 5 |   "scripts": {
 6 |     "dev": "next dev",
 7 |     "build": "next build",
 8 |     "start": "next start",
 9 |     "lint": "next lint"
10 |   },
11 |   "dependencies": {
12 |     "@radix-ui/react-slot": "^1.2.3",
13 |     "class-variance-authority": "^0.7.1",
14 |     "clsx": "^2.1.1",
15 |     "lucide-react": "^0.525.0",
16 |     "next": "^15.5.2",
17 |     "react": "^19.0.0",
18 |     "react-dom": "^19.0.0",
19 |     "tailwind-merge": "^3.3.1"
20 |   },
21 |   "devDependencies": {
22 |     "@tailwindcss/postcss": "^4",
23 |     "@types/node": "^20",
24 |     "@types/react": "^19",
25 |     "@types/react-dom": "^19",
26 |     "tailwindcss": "^4",
27 |     "tw-animate-css": "^1.3.5",
28 |     "typescript": "^5"
29 |   }
30 | }
31 | 


--------------------------------------------------------------------------------
/pages/_app.tsx:
--------------------------------------------------------------------------------
 1 | // pages/_app.tsx
 2 | 
 3 | import type { AppProps } from 'next/app'
 4 | import { Metadata } from 'next'
 5 | import '../app/globals.css'
 6 | import { UserProvider } from '@/context/userContext'
 7 | 
 8 | export const metadata: Metadata = {
 9 |     title: 'NextJs Starters',
10 |     description: '',
11 | }
12 | 
13 | function MyApp({ Component, pageProps }: AppProps) {
14 |     return (
15 |         <>
16 |             <UserProvider>
17 |                 <Component {...pageProps} />
18 |             </UserProvider>
19 |         </>
20 |     )
21 | }
22 | 
23 | export default MyApp
24 | 


--------------------------------------------------------------------------------
/pages/index.tsx:
--------------------------------------------------------------------------------
 1 | import React from 'react';
 2 | import Image from 'next/image';
 3 | 
 4 | const Index = () => {
 5 |     return (
 6 |         <div className="grid grid-rows-[20px_1fr_20px] items-center justify-items-center min-h-screen p-8 pb-20 gap-16 sm:p-20">
 7 |             <main className="flex flex-col gap-8 row-start-2 items-center sm:items-start">
 8 | 
 9 |                 <ul className="list-inside list-decimal text-xl text-center sm:text-left">
10 |                     <li>This is the starters pack for nextjs projects.</li>
11 |                 </ul>
12 | 
13 |             </main>
14 |             <footer className="row-start-3 flex gap-6 flex-wrap items-center justify-center">
15 |                 <a
16 |                     className="flex items-center gap-2 hover:underline hover:underline-offset-4"
17 |                     href="https://github.com/the-bipu"
18 |                     target="_blank"
19 |                     rel="noopener noreferrer"
20 |                 >
21 |                     <Image
22 |                         aria-hidden
23 |                         src="./globe.svg"
24 |                         alt="Globe icon"
25 |                         width={16}
26 |                         height={16}
27 |                     />
28 |                     Contact Us →
29 |                 </a>
30 |             </footer>
31 |         </div>
32 |     )
33 | }
34 | 
35 | export default Index


--------------------------------------------------------------------------------
/postcss.config.mjs:
--------------------------------------------------------------------------------
1 | const config = {
2 |   plugins: ["@tailwindcss/postcss"],
3 | };
4 | 
5 | export default config;
6 | 


--------------------------------------------------------------------------------
/public/file.svg:
--------------------------------------------------------------------------------
1 | <svg fill="none" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg"><path d="M14.5 13.5V5.41a1 1 0 0 0-.3-.7L9.8.29A1 1 0 0 0 9.08 0H1.5v13.5A2.5 2.5 0 0 0 4 16h8a2.5 2.5 0 0 0 2.5-2.5m-1.5 0v-7H8v-5H3v12a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1M9.5 5V2.12L12.38 5zM5.13 5h-.62v1.25h2.12V5zm-.62 3h7.12v1.25H4.5zm.62 3h-.62v1.25h7.12V11z" clip-rule="evenodd" fill="#666" fill-rule="evenodd"/></svg>


--------------------------------------------------------------------------------
/public/globe.svg:
--------------------------------------------------------------------------------
1 | <svg fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><g clip-path="url(#a)"><path fill-rule="evenodd" clip-rule="evenodd" d="M10.27 14.1a6.5 6.5 0 0 0 3.67-3.45q-1.24.21-2.7.34-.31 1.83-.97 3.1M8 16A8 8 0 1 0 8 0a8 8 0 0 0 0 16m.48-1.52a7 7 0 0 1-.96 0H7.5a4 4 0 0 1-.84-1.32q-.38-.89-.63-2.08a40 40 0 0 0 3.92 0q-.25 1.2-.63 2.08a4 4 0 0 1-.84 1.31zm2.94-4.76q1.66-.15 2.95-.43a7 7 0 0 0 0-2.58q-1.3-.27-2.95-.43a18 18 0 0 1 0 3.44m-1.27-3.54a17 17 0 0 1 0 3.64 39 39 0 0 1-4.3 0 17 17 0 0 1 0-3.64 39 39 0 0 1 4.3 0m1.1-1.17q1.45.13 2.69.34a6.5 6.5 0 0 0-3.67-3.44q.65 1.26.98 3.1M8.48 1.5l.01.02q.41.37.84 1.31.38.89.63 2.08a40 40 0 0 0-3.92 0q.25-1.2.63-2.08a4 4 0 0 1 .85-1.32 7 7 0 0 1 .96 0m-2.75.4a6.5 6.5 0 0 0-3.67 3.44 29 29 0 0 1 2.7-.34q.31-1.83.97-3.1M4.58 6.28q-1.66.16-2.95.43a7 7 0 0 0 0 2.58q1.3.27 2.95.43a18 18 0 0 1 0-3.44m.17 4.71q-1.45-.12-2.69-.34a6.5 6.5 0 0 0 3.67 3.44q-.65-1.27-.98-3.1" fill="#666"/></g><defs><clipPath id="a"><path fill="#fff" d="M0 0h16v16H0z"/></clipPath></defs></svg>


--------------------------------------------------------------------------------
/public/next.svg:
--------------------------------------------------------------------------------
1 | <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 394 80"><path fill="#000" d="M262 0h68.5v12.7h-27.2v66.6h-13.6V12.7H262V0ZM149 0v12.7H94v20.4h44.3v12.6H94v21h55v12.6H80.5V0h68.7zm34.3 0h-17.8l63.8 79.4h17.9l-32-39.7 32-39.6h-17.9l-23 28.6-23-28.6zm18.3 56.7-9-11-27.1 33.7h17.8l18.3-22.7z"/><path fill="#000" d="M81 79.3 17 0H0v79.3h13.6V17l50.2 62.3H81Zm252.6-.4c-1 0-1.8-.4-2.5-1s-1.1-1.6-1.1-2.6.3-1.8 1-2.5 1.6-1 2.6-1 1.8.3 2.5 1a3.4 3.4 0 0 1 .6 4.3 3.7 3.7 0 0 1-3 1.8zm23.2-33.5h6v23.3c0 2.1-.4 4-1.3 5.5a9.1 9.1 0 0 1-3.8 3.5c-1.6.8-3.5 1.3-5.7 1.3-2 0-3.7-.4-5.3-1s-2.8-1.8-3.7-3.2c-.9-1.3-1.4-3-1.4-5h6c.1.8.3 1.6.7 2.2s1 1.2 1.6 1.5c.7.4 1.5.5 2.4.5 1 0 1.8-.2 2.4-.6a4 4 0 0 0 1.6-1.8c.3-.8.5-1.8.5-3V45.5zm30.9 9.1a4.4 4.4 0 0 0-2-3.3 7.5 7.5 0 0 0-4.3-1.1c-1.3 0-2.4.2-3.3.5-.9.4-1.6 1-2 1.6a3.5 3.5 0 0 0-.3 4c.3.5.7.9 1.3 1.2l1.8 1 2 .5 3.2.8c1.3.3 2.5.7 3.7 1.2a13 13 0 0 1 3.2 1.8 8.1 8.1 0 0 1 3 6.5c0 2-.5 3.7-1.5 5.1a10 10 0 0 1-4.4 3.5c-1.8.8-4.1 1.2-6.8 1.2-2.6 0-4.9-.4-6.8-1.2-2-.8-3.4-2-4.5-3.5a10 10 0 0 1-1.7-5.6h6a5 5 0 0 0 3.5 4.6c1 .4 2.2.6 3.4.6 1.3 0 2.5-.2 3.5-.6 1-.4 1.8-1 2.4-1.7a4 4 0 0 0 .8-2.4c0-.9-.2-1.6-.7-2.2a11 11 0 0 0-2.1-1.4l-3.2-1-3.8-1c-2.8-.7-5-1.7-6.6-3.2a7.2 7.2 0 0 1-2.4-5.7 8 8 0 0 1 1.7-5 10 10 0 0 1 4.3-3.5c2-.8 4-1.2 6.4-1.2 2.3 0 4.4.4 6.2 1.2 1.8.8 3.2 2 4.3 3.4 1 1.4 1.5 3 1.5 5h-5.8z"/></svg>


--------------------------------------------------------------------------------
/public/vercel.svg:
--------------------------------------------------------------------------------
1 | <svg fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1155 1000"><path d="m577.3 0 577.4 1000H0z" fill="#fff"/></svg>


--------------------------------------------------------------------------------
/public/window.svg:
--------------------------------------------------------------------------------
1 | <svg fill="none" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill-rule="evenodd" clip-rule="evenodd" d="M1.5 2.5h13v10a1 1 0 0 1-1 1h-11a1 1 0 0 1-1-1zM0 1h16v11.5a2.5 2.5 0 0 1-2.5 2.5h-11A2.5 2.5 0 0 1 0 12.5zm3.75 4.5a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5M7 4.75a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0m1.75.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5" fill="#666"/></svg>


--------------------------------------------------------------------------------
/tsconfig.json:
--------------------------------------------------------------------------------
 1 | {
 2 |   "compilerOptions": {
 3 |     "target": "ES2017",
 4 |     "lib": ["dom", "dom.iterable", "esnext"],
 5 |     "allowJs": true,
 6 |     "skipLibCheck": true,
 7 |     "strict": true,
 8 |     "noEmit": true,
 9 |     "esModuleInterop": true,
10 |     "module": "esnext",
11 |     "moduleResolution": "bundler",
12 |     "resolveJsonModule": true,
13 |     "isolatedModules": true,
14 |     "jsx": "preserve",
15 |     "incremental": true,
16 |     "plugins": [
17 |       {
18 |         "name": "next"
19 |       }
20 |     ],
21 |     "paths": {
22 |       "@/*": ["./*"]
23 |     }
24 |   },
25 |   "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
26 |   "exclude": ["node_modules"]
27 | }
28 | 


--------------------------------------------------------------------------------
