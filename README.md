# Choice Properties Lease Intelligence Platform

I've successfully built the Choice Properties Lease Intelligence Platform following the Vercel architecture and requirements.

## Architecture Highlights
- **Framework**: Next.js 14+ with App Router and Tailwind CSS + `shadcn/ui`.
- **Pages Built**:
  - `/`: Main RAG chat interface with suggested prompts, citation chips, and a slide-over lease detail drawer.
  - `/portfolio`: Analytics dashboard with KPI cards, Recharts visualizations, and a TanStack react-table showing the full corpus.
  - `/about`: Executive-level explanation of the architecture with a bold synthetic-data disclaimer.
- **RAG & Search**:
  - Implementation of a custom hybrid search via `lib/retrieval.ts`.
  - Intent classification (`lib/intent.ts`) routes queries as `structured`, `semantic`, or `hybrid` seamlessly.
- **Streaming UI**: Server-side generation and client-side stream consumption via Vercel AI SDK.

## Setup & Demo Instructions

> [!IMPORTANT]
> Because you need to provide your own OpenAI API Key, you must run the data ingestion step before the chat will work.

1. Create a `.env.local` file by copying the provided example:
   ```bash
   cp .env.local.example .env.local
   ```
2. Open `.env.local` and add your `OPENAI_API_KEY`.
3. Run the ingestion script to parse the CSV and generate embeddings (this will generate `data/leases.json` and `data/embeddings.json`):
   ```bash
   npm run ingest
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```

## Vercel Deployment
To deploy this straight to Vercel:
1. Push the code to a GitHub repository or link your Vercel CLI via `vercel`.
2. Add your `OPENAI_API_KEY` to the Vercel Environment Variables in the project dashboard.
3. Deploy. Because the `embeddings.json` and `leases.json` are committed to the `/data` folder (after running `npm run ingest`), they will automatically be bundled into your Vercel serverless deployment! No external database required.
