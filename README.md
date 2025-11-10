# PriceSight
/*
PriceSight - Single-file React prototype (Tailwind + Framer Motion)

WHAT THIS FILE IS:
- A single-file React component (default export) that is a complete, responsive marketing + product dashboard prototype for the "Narxlarni uydan chiqmasdan aniqlash" startup.
- Uses Tailwind utility classes and Framer Motion for light animations. Assumes Tailwind is configured in the project.
- Includes sections: Hero, Features, Live Demo (MVP), Tech Architecture, API contract (mock), Pricing, Roadmap, Team/Contact, Footer.

HOW TO USE:
1) Create a new React project (Vite or Next.js). Install dependencies:
   npm install react framer-motion lucide-react
   (Tailwind must be configured separately)
2) Save this file as src/App.jsx (or pages/index.jsx for Next.js) and run dev server.

SAMPLE API CONTRACT (mock) - keep on backend as /api
GET  /api/prices?query={q}&location={lat,lon}&page=1
  -> { data: [{id, name, store, price, currency, updated_at, url}], meta }
POST /api/alerts  { userId, productId, targetPrice }
  -> { status: 'ok', alertId }
GET  /api/trends?productId={id}&range=30d
  -> { trend: [{date, avgPrice}] }

MVP IMPLEMENTATION NOTES
- Data ingestion: scrapers + store APIs
- DB: PostgreSQL for structured data; Redis for cache
- Search & ranking: Elasticsearch / OpenSearch for fast filtering
- AI: small forecasting model to predict 7-30d price trend
- Auth: JWT + refresh tokens

---- START OF REACT COMPONENT ----
*/

import React from 'react'
import { motion } from 'framer-motion'
import { Search, ShoppingCart, Database, Cloud, Clock, Zap, Users, Mail } from 'lucide-react'

export default function App () {
  const features = [
    { title: 'Real-time Price Aggregation', desc: 'Onlayn va oflayn manbalardan narxlar: dokon kataloglari, marketlar va yetkazib beruvchilar.', icon: <Database size={28} /> },
    { title: 'AI Trend Forecasting', desc: 'Suniy intellekt yordamida narx tendensiyalarini prognoz qilamiz  eng yaxshi xarid vaqtini korsatamiz.', icon: <Zap size={28} /> },
    { title: 'Location-aware Filters', desc: 'Joylashuvga mos filtr, yetkazib berish vaqti va marka boyicha saralash.', icon: <Clock size={28} /> },
    { title: 'Alerts & Subscriptions', desc: 'Narx tushganda ogohlantirishlar va premium analitika.', icon: <Mail size={28} /> }
  ]

  const tech = [
    { name: 'Scrapers & Integrations', desc: 'Headless browsers, site-specific scrapers, and store APIs.' },
    { name: 'API & Backend', desc: 'FastAPI / Node.js with PostgreSQL and Redis caching.' },
    { name: 'Search', desc: 'OpenSearch / Elasticsearch for fast filtering and analytics.' },
    { name: 'AI/Forecasting', desc: 'Lightweight time-series models for 7-30 day forecasts.' }
  ]

  const roadmap = [
    { quarter: 'Q1', items: ['MVP: core scrapers, API, basic UI', 'Pilot with local stores'] },
    { quarter: 'Q2', items: ['Premium alerts', 'Seller dashboard & API monetization'] },
    { quarter: 'Q3', items: ['Scaling to regional markets', 'Mobile app beta'] },
    { quarter: 'Q4', items: ['Analytics product for businesses', 'Investor round'] }
  ]

  return (
    <div className="min-h-screen bg-gray-50 text-slate-900">
      <header className="bg-white shadow-sm sticky top-0 z-30">
        <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="rounded-full bg-gradient-to-r from-indigo-600 to-teal-400 p-2 text-white">
              <ShoppingCart size={20} />
            </div>
            <div>
              <h1 className="text-xl font-semibold">PriceSight</h1>
              <p className="text-xs text-slate-500">Narxlarni uydan chiqmasdan aniqlash</p>
            </div>
          </div>

          <nav className="hidden md:flex items-center gap-6 text-sm text-slate-700">
            <a href="#features" className="hover:text-slate-900">Xususiyatlar</a>
            <a href="#tech" className="hover:text-slate-900">Texnologiya</a>
            <a href="#pricing" className="hover:text-slate-900">Narxlar</a>
            <a href="#roadmap" className="hover:text-slate-900">Yo'l xaritasi</a>
            <a href="#contact" className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Bog'lanish</a>
          </nav>

          <div className="md:hidden">{/* mobile menu placeholder */}
            <button aria-label="menu" className="p-2 rounded-lg bg-slate-100"><Search size={18} /></button>
          </div>
        </div>
      </header>

      <main className="max-w-7xl mx-auto px-6 py-16">
        <section className="grid md:grid-cols-2 gap-8 items-center">
          <motion.div initial={{ x: -40, opacity: 0 }} animate={{ x: 0, opacity: 1 }} transition={{ duration: 0.6 }}>
            <h2 className="text-4xl font-extrabold leading-tight">Eng yaxshi narxni toping — uydan chiqmasdan</h2>
            <p className="mt-4 text-slate-600">Bir joyda barcha do'konlar va yetkazib beruvchilardan real-vaqt narxlarni ko'ring, ogohlantirishlar o'rnating va narx tendensiyalarini kuzating.</p>

            <div className="mt-6 flex gap-3">
              <a href="#mvp" className="px-5 py-3 rounded-lg bg-indigo-600 text-white font-medium">MVP-ni ko'rish</a>
              <a href="#pricing" className="px-5 py-3 rounded-lg border border-slate-200 text-slate-700">Bepul boshlash</a>
            </div>

            <div className="mt-8 grid grid-cols-2 gap-3 text-sm text-slate-600">
              <div className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3"><Cloud size={18} /><div>Real-time updates</div></div>
              </div>
              <div className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3"><Users size={18} /><div>Biznes va oddiy foydalanuvchi rejalari</div></div>
              </div>
            </div>
          </motion.div>

          <motion.div initial={{ scale: 0.95, opacity: 0 }} animate={{ scale: 1, opacity: 1 }} transition={{ duration: 0.6 }}>
            {/* Mock search UI / live demo card */}
            <div id="mvp" className="bg-white rounded-2xl p-6 shadow-lg">
              <div className="flex items-center justify-between">
                <div>
                  <h3 className="font-semibold">Quick price search</h3>
                  <p className="text-xs text-slate-500">Namuna: "Samsung A15" — 13 ta natija</p>
                </div>
                <div className="text-xs text-slate-400">API v0.1</div>
              </div>

              <div className="mt-4">
                <div className="flex gap-2 items-center">
                  <input className="flex-1 border p-3 rounded-lg" placeholder="Mahsulot nomi, model yoki do'kon" />
                  <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Qidirish</button>
                </div>

                <div className="mt-4 grid gap-3">
                  {/* sample result */}
                  <div className="p-3 rounded-lg border flex items-center justify-between">
                    <div>
                      <div className="font-medium">Samsung A15 - 128GB</div>
                      <div className="text-xs text-slate-500">Do'kon: TechStore • Yangilangan: 2 soat oldin</div>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">2,999,000 so'm</div>
                      <div className="text-xs text-slate-400">Yetkazib berish: 2-3 kun</div>
                    </div>
                  </div>

                  <div className="p-3 rounded-lg border flex items-center justify-between">
                    <div>
                      <div className="font-medium">Samsung A15 - 128GB</div>
                      <div className="text-xs text-slate-500">Do'kon: MobileKing • Yangilangan: 1 kun oldin</div>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">3,050,000 so'm</div>
                      <div className="text-xs text-slate-400">Pickup mavjud</div>
                    </div>
                  </div>
                </div>

                <div className="mt-4 text-xs text-slate-500">(Bu demo — statik namunadir; real MVP server + scrapers talab qiladi.)</div>
              </div>
            </div>
          </motion.div>
        </section>

        <section id="features" className="mt-16">
          <h3 className="text-2xl font-bold">Xususiyatlar</h3>
          <p className="mt-2 text-slate-600">Bizning yechim foydalanuvchi va biznes uchun qulay imkoniyatlarni taqdim etadi.</p>

          <div className="mt-6 grid md:grid-cols-4 gap-4">
            {features.map((f) => (
              <div key={f.title} className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3">
                  <div className="p-2 bg-slate-100 rounded-md">{f.icon}</div>
                  <div>
                    <div className="font-semibold">{f.title}</div>
                    <div className="text-sm text-slate-500">{f.desc}</div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </section>

        <section id="tech" className="mt-16">
          <h3 className="text-2xl font-bold">Texnologiya arxitekturasi</h3>
          <p className="mt-2 text-slate-600">Qisqacha ko'rinish: ma'lumot yig'ish → konsolidatsiya → indekslash → API → UI.</p>

          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Stack</h4>
              <ul className="mt-3 text-sm text-slate-600 space-y-2">
                {tech.map(t => <li key={t.name}><span className="font-medium">{t.name}:</span> {t.desc}</li>)}
              </ul>
            </div>

            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Scaling & Security</h4>
              <p className="text-sm text-slate-600 mt-2">Bulutda microservices, autoscaling, rolga asoslangan kirish boshqaruvi (RBAC), va ma'lumotlar shifrlash.</p>

              <div className="mt-4 grid gap-2">
                <div className="text-sm">Cache: Redis</div>
                <div className="text-sm">Search: OpenSearch</div>
                <div className="text-sm">DB: PostgreSQL</div>
              </div>
            </div>
          </div>
        </section>

        <section id="pricing" className="mt-16">
          <h3 className="text-2xl font-bold">Narxlar</h3>
          <p className="mt-2 text-slate-600">Freemium + Premium obuna va biznes paketlari.</p>

          <div className="mt-6 grid md:grid-cols-3 gap-4">
            <div className="p-6 bg-white rounded-lg shadow-sm">
              <div className="text-sm text-slate-500">BEPUL</div>
              <div className="text-2xl font-bold mt-2">0 so'm/oy</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>Asosiy qidiruv</li>
                <li>1 ogohlantirish</li>
                <li>7 kun narx tarixi</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg border">Ro'yxatdan o'tish</button>
            </div>

            <div className="p-6 bg-white rounded-lg shadow-sm border-2 border-indigo-100">
              <div className="text-sm text-slate-500">PRO</div>
              <div className="text-2xl font-bold mt-2">39,000 so'm/oy</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>Cheksiz ogohlantirishlar</li>
                <li>30 kun narx tarixi</li>
                <li>API kirish (cheklangan)</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg bg-indigo-600 text-white">Premiumga o'tish</button>
            </div>

            <div className="p-6 bg-white rounded-lg shadow-sm">
              <div className="text-sm text-slate-500">BUSINESS</div>
              <div className="text-2xl font-bold mt-2">So'rov asosida</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>API & Data Feed</li>
                <li>Custom scraping</li>
                <li>SLAs & Analytics</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg border">So'rov yuborish</button>
            </div>
          </div>
        </section>

        <section id="roadmap" className="mt-16">
          <h3 className="text-2xl font-bold">Yo'l xaritasi</h3>
          <div className="mt-6 grid md:grid-cols-4 gap-4">
            {roadmap.map(r => (
              <div key={r.quarter} className="p-4 bg-white rounded-lg shadow-sm">
                <div className="font-semibold">{r.quarter}</div>
                <ul className="mt-3 text-sm text-slate-600 space-y-2">
                  {r.items.map(i => <li key={i}>• {i}</li>)}
                </ul>
              </div>
            ))}
          </div>
        </section>

        <section id="api" className="mt-16 bg-gradient-to-r from-slate-50 to-white p-6 rounded-xl border">
          <h3 className="text-2xl font-bold">API & Developer Quickstart</h3>
          <p className="mt-2 text-slate-600">Minimal API kontrakt (mock) — backendni shu asosda quramiz.</p>

          <pre className="mt-4 overflow-auto bg-slate-900 text-slate-100 p-4 rounded">
{`GET /api/prices?query=Samsung&page=1&lat=41.3&lon=69.2
Response: { data: [{ id, name, store, price, currency, updated_at, url }], meta }

POST /api/alerts
Body: { userId, productId, targetPrice }
Response: { status: 'ok', alertId }
`}
          </pre>

          <div className="mt-4 text-sm text-slate-600">Qo'shimcha: OAuth2, rate limits, webhooks for partners.</div>
        </section>

        <section id="contact" className="mt-16">
          <h3 className="text-2xl font-bold">Bog'lanish</h3>
          <p className="mt-2 text-slate-600">Investorlar, do'kon hamkorliklari yoki pilotni boshlash uchun biz bilan bog'laning.</p>

          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Jamoa</h4>
              <p className="mt-2 text-sm text-slate-600">Mahsulot boshqaruvi, data engineering, va growth marketing bilan to'liq jamoa.</p>

              <div className="mt-4 text-sm">
                <div>CEO: Alisher</div>
                <div>CTO: Nodir</div>
                <div>BizDev: Dilshod</div>
              </div>
            </div>

            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Kontakt</h4>
              <form className="mt-3 grid gap-3">
                <input className="border p-2 rounded" placeholder="Ismingiz" />
                <input className="border p-2 rounded" placeholder="Email" />
                <textarea className="border p-2 rounded" placeholder="Xabar..." rows={4} />
                <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Yuborish</button>
              </form>
            </div>
          </div>
        </section>

      </main>

      <footer className="mt-16 bg-white border-t">
        <div className="max-w-7xl mx-auto px-6 py-8 flex flex-col md:flex-row items-center justify-between gap-4">
          <div className="text-sm text-slate-600">© {new Date().getFullYear()} PriceSight — Narxlarni uydan chiqmasdan aniqlash</div>
          <div className="flex items-center gap-4 text-sm text-slate-600">
            <a href="#">GitHub</a>
            <a href="#">Pitch Deck</a>
            <a href="#">Privacy</a>
          </div>
        </div>
      </footer>
    </div>
  )
}
/*
PriceSight - Single-file React prototype (Tailwind + Framer Motion)

WHAT THIS FILE IS:
- A single-file React component (default export) that is a complete, responsive marketing + product dashboard prototype for the "Narxlarni uydan chiqmasdan aniqlash" startup.
- Uses Tailwind utility classes and Framer Motion for light animations. Assumes Tailwind is configured in the project.
- Includes sections: Hero, Features, Live Demo (MVP), Tech Architecture, API contract (mock), Pricing, Roadmap, Team/Contact, Footer.

HOW TO USE:
1) Create a new React project (Vite or Next.js). Install dependencies:
   npm install react framer-motion lucide-react
   (Tailwind must be configured separately)
2) Save this file as src/App.jsx (or pages/index.jsx for Next.js) and run dev server.

SAMPLE API CONTRACT (mock) - keep on backend as /api
GET  /api/prices?query={q}&location={lat,lon}&page=1
  -> { data: [{id, name, store, price, currency, updated_at, url}], meta }
POST /api/alerts  { userId, productId, targetPrice }
  -> { status: 'ok', alertId }
GET  /api/trends?productId={id}&range=30d
  -> { trend: [{date, avgPrice}] }

MVP IMPLEMENTATION NOTES
- Data ingestion: scrapers + store APIs
- DB: PostgreSQL for structured data; Redis for cache
- Search & ranking: Elasticsearch / OpenSearch for fast filtering
- AI: small forecasting model to predict 7-30d price trend
- Auth: JWT + refresh tokens

---- START OF REACT COMPONENT ----
*/

import React from 'react'
import { motion } from 'framer-motion'
import { Search, ShoppingCart, Database, Cloud, Clock, Zap, Users, Mail } from 'lucide-react'

export default function App () {
  const features = [
    { title: 'Real-time Price Aggregation', desc: 'Onlayn va oflayn manbalardan narxlar: dokon kataloglari, marketlar va yetkazib beruvchilar.', icon: <Database size={28} /> },
    { title: 'AI Trend Forecasting', desc: 'Suniy intellekt yordamida narx tendensiyalarini prognoz qilamiz  eng yaxshi xarid vaqtini korsatamiz.', icon: <Zap size={28} /> },
    { title: 'Location-aware Filters', desc: 'Joylashuvga mos filtr, yetkazib berish vaqti va marka boyicha saralash.', icon: <Clock size={28} /> },
    { title: 'Alerts & Subscriptions', desc: 'Narx tushganda ogohlantirishlar va premium analitika.', icon: <Mail size={28} /> }
  ]

  const tech = [
    { name: 'Scrapers & Integrations', desc: 'Headless browsers, site-specific scrapers, and store APIs.' },
    { name: 'API & Backend', desc: 'FastAPI / Node.js with PostgreSQL and Redis caching.' },
    { name: 'Search', desc: 'OpenSearch / Elasticsearch for fast filtering and analytics.' },
    { name: 'AI/Forecasting', desc: 'Lightweight time-series models for 7-30 day forecasts.' }
  ]

  const roadmap = [
    { quarter: 'Q1', items: ['MVP: core scrapers, API, basic UI', 'Pilot with local stores'] },
    { quarter: 'Q2', items: ['Premium alerts', 'Seller dashboard & API monetization'] },
    { quarter: 'Q3', items: ['Scaling to regional markets', 'Mobile app beta'] },
    { quarter: 'Q4', items: ['Analytics product for businesses', 'Investor round'] }
  ]

  return (
    <div className="min-h-screen bg-gray-50 text-slate-900">
      <header className="bg-white shadow-sm sticky top-0 z-30">
        <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="rounded-full bg-gradient-to-r from-indigo-600 to-teal-400 p-2 text-white">
              <ShoppingCart size={20} />
            </div>
            <div>
              <h1 className="text-xl font-semibold">PriceSight</h1>
              <p className="text-xs text-slate-500">Narxlarni uydan chiqmasdan aniqlash</p>
            </div>
          </div>

          <nav className="hidden md:flex items-center gap-6 text-sm text-slate-700">
            <a href="#features" className="hover:text-slate-900">Xususiyatlar</a>
            <a href="#tech" className="hover:text-slate-900">Texnologiya</a>
            <a href="#pricing" className="hover:text-slate-900">Narxlar</a>
            <a href="#roadmap" className="hover:text-slate-900">Yo'l xaritasi</a>
            <a href="#contact" className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Bog'lanish</a>
          </nav>

          <div className="md:hidden">{/* mobile menu placeholder */}
            <button aria-label="menu" className="p-2 rounded-lg bg-slate-100"><Search size={18} /></button>
          </div>
        </div>
      </header>

      <main className="max-w-7xl mx-auto px-6 py-16">
        <section className="grid md:grid-cols-2 gap-8 items-center">
          <motion.div initial={{ x: -40, opacity: 0 }} animate={{ x: 0, opacity: 1 }} transition={{ duration: 0.6 }}>
            <h2 className="text-4xl font-extrabold leading-tight">Eng yaxshi narxni toping — uydan chiqmasdan</h2>
            <p className="mt-4 text-slate-600">Bir joyda barcha do'konlar va yetkazib beruvchilardan real-vaqt narxlarni ko'ring, ogohlantirishlar o'rnating va narx tendensiyalarini kuzating.</p>

            <div className="mt-6 flex gap-3">
              <a href="#mvp" className="px-5 py-3 rounded-lg bg-indigo-600 text-white font-medium">MVP-ni ko'rish</a>
              <a href="#pricing" className="px-5 py-3 rounded-lg border border-slate-200 text-slate-700">Bepul boshlash</a>
            </div>

            <div className="mt-8 grid grid-cols-2 gap-3 text-sm text-slate-600">
              <div className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3"><Cloud size={18} /><div>Real-time updates</div></div>
              </div>
              <div className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3"><Users size={18} /><div>Biznes va oddiy foydalanuvchi rejalari</div></div>
              </div>
            </div>
          </motion.div>

          <motion.div initial={{ scale: 0.95, opacity: 0 }} animate={{ scale: 1, opacity: 1 }} transition={{ duration: 0.6 }}>
            {/* Mock search UI / live demo card */}
            <div id="mvp" className="bg-white rounded-2xl p-6 shadow-lg">
              <div className="flex items-center justify-between">
                <div>
                  <h3 className="font-semibold">Quick price search</h3>
                  <p className="text-xs text-slate-500">Namuna: "Samsung A15" — 13 ta natija</p>
                </div>
                <div className="text-xs text-slate-400">API v0.1</div>
              </div>

              <div className="mt-4">
                <div className="flex gap-2 items-center">
                  <input className="flex-1 border p-3 rounded-lg" placeholder="Mahsulot nomi, model yoki do'kon" />
                  <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Qidirish</button>
                </div>

                <div className="mt-4 grid gap-3">
                  {/* sample result */}
                  <div className="p-3 rounded-lg border flex items-center justify-between">
                    <div>
                      <div className="font-medium">Samsung A15 - 128GB</div>
                      <div className="text-xs text-slate-500">Do'kon: TechStore • Yangilangan: 2 soat oldin</div>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">2,999,000 so'm</div>
                      <div className="text-xs text-slate-400">Yetkazib berish: 2-3 kun</div>
                    </div>
                  </div>

                  <div className="p-3 rounded-lg border flex items-center justify-between">
                    <div>
                      <div className="font-medium">Samsung A15 - 128GB</div>
                      <div className="text-xs text-slate-500">Do'kon: MobileKing • Yangilangan: 1 kun oldin</div>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">3,050,000 so'm</div>
                      <div className="text-xs text-slate-400">Pickup mavjud</div>
                    </div>
                  </div>
                </div>

                <div className="mt-4 text-xs text-slate-500">(Bu demo — statik namunadir; real MVP server + scrapers talab qiladi.)</div>
              </div>
            </div>
          </motion.div>
        </section>

        <section id="features" className="mt-16">
          <h3 className="text-2xl font-bold">Xususiyatlar</h3>
          <p className="mt-2 text-slate-600">Bizning yechim foydalanuvchi va biznes uchun qulay imkoniyatlarni taqdim etadi.</p>

          <div className="mt-6 grid md:grid-cols-4 gap-4">
            {features.map((f) => (
              <div key={f.title} className="p-4 bg-white rounded-lg shadow-sm">
                <div className="flex items-center gap-3">
                  <div className="p-2 bg-slate-100 rounded-md">{f.icon}</div>
                  <div>
                    <div className="font-semibold">{f.title}</div>
                    <div className="text-sm text-slate-500">{f.desc}</div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </section>

        <section id="tech" className="mt-16">
          <h3 className="text-2xl font-bold">Texnologiya arxitekturasi</h3>
          <p className="mt-2 text-slate-600">Qisqacha ko'rinish: ma'lumot yig'ish → konsolidatsiya → indekslash → API → UI.</p>

          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Stack</h4>
              <ul className="mt-3 text-sm text-slate-600 space-y-2">
                {tech.map(t => <li key={t.name}><span className="font-medium">{t.name}:</span> {t.desc}</li>)}
              </ul>
            </div>

            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Scaling & Security</h4>
              <p className="text-sm text-slate-600 mt-2">Bulutda microservices, autoscaling, rolga asoslangan kirish boshqaruvi (RBAC), va ma'lumotlar shifrlash.</p>

              <div className="mt-4 grid gap-2">
                <div className="text-sm">Cache: Redis</div>
                <div className="text-sm">Search: OpenSearch</div>
                <div className="text-sm">DB: PostgreSQL</div>
              </div>
            </div>
          </div>
        </section>

        <section id="pricing" className="mt-16">
          <h3 className="text-2xl font-bold">Narxlar</h3>
          <p className="mt-2 text-slate-600">Freemium + Premium obuna va biznes paketlari.</p>

          <div className="mt-6 grid md:grid-cols-3 gap-4">
            <div className="p-6 bg-white rounded-lg shadow-sm">
              <div className="text-sm text-slate-500">BEPUL</div>
              <div className="text-2xl font-bold mt-2">0 so'm/oy</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>Asosiy qidiruv</li>
                <li>1 ogohlantirish</li>
                <li>7 kun narx tarixi</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg border">Ro'yxatdan o'tish</button>
            </div>

            <div className="p-6 bg-white rounded-lg shadow-sm border-2 border-indigo-100">
              <div className="text-sm text-slate-500">PRO</div>
              <div className="text-2xl font-bold mt-2">39,000 so'm/oy</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>Cheksiz ogohlantirishlar</li>
                <li>30 kun narx tarixi</li>
                <li>API kirish (cheklangan)</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg bg-indigo-600 text-white">Premiumga o'tish</button>
            </div>

            <div className="p-6 bg-white rounded-lg shadow-sm">
              <div className="text-sm text-slate-500">BUSINESS</div>
              <div className="text-2xl font-bold mt-2">So'rov asosida</div>
              <ul className="mt-4 text-sm text-slate-600 space-y-2">
                <li>API & Data Feed</li>
                <li>Custom scraping</li>
                <li>SLAs & Analytics</li>
              </ul>
              <button className="mt-4 px-4 py-2 rounded-lg border">So'rov yuborish</button>
            </div>
          </div>
        </section>

        <section id="roadmap" className="mt-16">
          <h3 className="text-2xl font-bold">Yo'l xaritasi</h3>
          <div className="mt-6 grid md:grid-cols-4 gap-4">
            {roadmap.map(r => (
              <div key={r.quarter} className="p-4 bg-white rounded-lg shadow-sm">
                <div className="font-semibold">{r.quarter}</div>
                <ul className="mt-3 text-sm text-slate-600 space-y-2">
                  {r.items.map(i => <li key={i}>• {i}</li>)}
                </ul>
              </div>
            ))}
          </div>
        </section>

        <section id="api" className="mt-16 bg-gradient-to-r from-slate-50 to-white p-6 rounded-xl border">
          <h3 className="text-2xl font-bold">API & Developer Quickstart</h3>
          <p className="mt-2 text-slate-600">Minimal API kontrakt (mock) — backendni shu asosda quramiz.</p>

          <pre className="mt-4 overflow-auto bg-slate-900 text-slate-100 p-4 rounded">
{`GET /api/prices?query=Samsung&page=1&lat=41.3&lon=69.2
Response: { data: [{ id, name, store, price, currency, updated_at, url }], meta }

POST /api/alerts
Body: { userId, productId, targetPrice }
Response: { status: 'ok', alertId }
`}
          </pre>

          <div className="mt-4 text-sm text-slate-600">Qo'shimcha: OAuth2, rate limits, webhooks for partners.</div>
        </section>

        <section id="contact" className="mt-16">
          <h3 className="text-2xl font-bold">Bog'lanish</h3>
          <p className="mt-2 text-slate-600">Investorlar, do'kon hamkorliklari yoki pilotni boshlash uchun biz bilan bog'laning.</p>

          <div className="mt-6 grid md:grid-cols-2 gap-6">
            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Jamoa</h4>
              <p className="mt-2 text-sm text-slate-600">Mahsulot boshqaruvi, data engineering, va growth marketing bilan to'liq jamoa.</p>

              <div className="mt-4 text-sm">
                <div>CEO: Alisher</div>
                <div>CTO: Nodir</div>
                <div>BizDev: Dilshod</div>
              </div>
            </div>

            <div className="bg-white p-6 rounded-lg shadow-sm">
              <h4 className="font-semibold">Kontakt</h4>
              <form className="mt-3 grid gap-3">
                <input className="border p-2 rounded" placeholder="Ismingiz" />
                <input className="border p-2 rounded" placeholder="Email" />
                <textarea className="border p-2 rounded" placeholder="Xabar..." rows={4} />
                <button className="px-4 py-2 rounded-lg bg-indigo-600 text-white">Yuborish</button>
              </form>
            </div>
          </div>
        </section>

      </main>

      <footer className="mt-16 bg-white border-t">
        <div className="max-w-7xl mx-auto px-6 py-8 flex flex-col md:flex-row items-center justify-between gap-4">
          <div className="text-sm text-slate-600">© {new Date().getFullYear()} PriceSight — Narxlarni uydan chiqmasdan aniqlash</div>
          <div className="flex items-center gap-4 text-sm text-slate-600">
            <a href="#">GitHub</a>
            <a href="#">Pitch Deck</a>
            <a href="#">Privacy</a>
          </div>
        </div>
      </footer>
    </div>
  )
}
