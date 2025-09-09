# 📊 Log Search Dashboard

A **lightweight alternative to ELK/Kibana**, built with **React, TailwindCSS, React Query**, and ready for **OpenSearch integration**.  
Easily dump logs, run queries, and explore results in a **fast and minimal UI**.  

---

## ✨ Features  

- 🔍 **Log Search** — filter by severity, source, project, and time range.  
- ⚡ **React Query + Axios** — efficient API data fetching with caching.  
- 🎨 **Modern UI** — dark mode, shadcn/ui components, TailwindCSS styling.  
- 📡 **Real-Time Mode** — optional tailing of logs (stream-like).  
- 🔗 **OpenSearch Ready** — mock API included, swap in your own OpenSearch endpoint.  
- 🛠️ **Developer Friendly** — simple, modular architecture.  

---

## 🚀 Getting Started  

### 1. Clone the Repo
```bash
git clone https://github.com/dostontech/logSearchDashboard.git
cd logSearchDashboard
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Start Mock Backend
```bash
node mock-server.js
```
Runs a small Express server at [http://localhost:4000/logs](http://localhost:4000/logs) to simulate log data.  

### 4. Start Frontend
```bash
npm run dev
```
The dashboard will be available at [http://localhost:5173](http://localhost:5173).  

---

## 🏗️ Project Structure  

```
log-search-dashboard/
├── src/
│   ├── components/   # UI Components (Navbar, FilterBar, LogTable)
│   ├── hooks/        # React Query hooks (useLogs, etc.)
│   ├── lib/          # API clients and helpers
│   ├── pages/        # Page-level layouts (Dashboard)
│   ├── App.tsx       # App entry
│   └── main.tsx      # React bootstrap
├── mock-server.js    # Mock backend (replace with OpenSearch)
├── tailwind.config.js
├── package.json
└── README.md
```

---

## 🔌 OpenSearch Integration  

To connect to OpenSearch:  

1. Configure your **OpenSearch endpoint** in `src/lib/api.ts`:  
   ```ts
   export const api = axios.create({
     baseURL: "https://your-opensearch-endpoint",
     auth: {
       username: "your-user",
       password: "your-pass"
     }
   });
   ```

2. Replace the mock `/logs` API call in `useLogs.ts` with an OpenSearch query:  
   ```ts
   queryFn: async () => {
     const res = await api.post("/_search", {
       query: {
         match: { severity }
       },
       sort: [{ "@timestamp": { order: "desc" } }]
     });
     return res.data.hits.hits.map((hit: any) => hit._source);
   }
   ```

---

## 🗺️ Roadmap  

- [ ] 🔄 Tail Mode (real-time streaming logs)  
- [ ] 📂 Multi-Project Support  
- [ ] 📊 Log Metrics + Charts  
- [ ] 🔐 Auth (JWT / OAuth2 for enterprise use)  
- [ ] 📦 Docker Compose (Frontend + API + OpenSearch)  

---

## 🤝 Contributing  

Contributions welcome! 🎉  
- Fork the repo  
- Create a feature branch (`git checkout -b feature/xyz`)  
- Commit changes (`git commit -m "Add xyz feature"`)  
- Push to your fork & create a PR  

---

## 📜 License  

MIT © 2025 — Built with ❤️ for teams who want **search without the Kibana overhead**  
