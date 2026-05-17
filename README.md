# 📄 Dynamic Portfolio + CV with JSONBin CMS

A fully responsive, single‑page portfolio and CV website with a built‑in admin panel and cloud‑based content management via [JSONBin.io](https://jsonbin.io).  
The frontend (`index.html`) displays your CV dynamically; the admin panel (`admin.html`) lets you edit everything – including hero section, work experience, skills, education, achievements, and contact details – and syncs the changes to a JSONBin backend.  
All visitors see the latest version instantly, across any device.

![Preview](https://via.placeholder.com/800x400?text=Portfolio+Screenshot)  
*(Replace with an actual screenshot of your portfolio)*

---

## ✨ Features

- **Fully editable CV** – No coding required to update your content.  
- **Cloud‑powered** – Content stored on JSONBin (free tier works thanks to automatic compression & chunking).  
- **Cross‑device sync** – Changes made in the admin panel appear immediately on your live site for every visitor.  
- **Responsive design** – Looks great on desktop, tablet, and mobile.  
- **Automatic chunking** – Bypasses JSONBin’s 100KB limit for free accounts (data is compressed and split into multiple bins if needed).  
- **Photo upload** – Add or remove your profile picture directly in the admin panel.  
- **Secure admin area** – Password‑protected editor (default: `admin123`, can be changed).  
- **Downloadable CV** – Option to provide a PDF download link.  
- **Contact form** – Visitors can email you directly (uses `mailto:`).  
- **Intersection animations** – Smooth fade‑in effects as you scroll.

---

## 🛠️ Tech Stack

- **Frontend** – HTML5, CSS3, Vanilla JavaScript  
- **CMS Backend** – [JSONBin.io](https://jsonbin.io) (REST API)  
- **Compression** – [lz‑string](https://github.com/pieroxy/lz-string) for efficient storage  
- **Fonts** – Google Fonts (Playfair Display, DM Sans)  
- **Hosting** – GitHub Pages (or any static web host)

---

## 🚀 Getting Started

### Prerequisites
- A free [JSONBin.io](https://jsonbin.io) account.  
- A GitHub account (to host the files).  

### Installation

1. **Clone or download** this repository.

2. **Create a bin on JSONBin**  
   - Log in to [jsonbin.io](https://jsonbin.io).  
   - Click **Create Bin** → name it (e.g., `my-cv-data`).  
   - Copy the **Bin ID** from the URL or the bin’s page.  
   - Copy your **API Key** (X‑Master‑Key) from your account settings.

3. **Configure the admin panel**  
   - Open `admin.html` in your browser (local or served).  
   - Log in with the default password: `admin123`.  
   - Go to the **Security & JSONBin** panel.  
   - Paste your **Bin ID** and **API Key**, then click **Save Config**.  
   - Click **Push to JSONBin** – this uploads the default CV structure to your bin.  
   - (Optional) Change the admin password in the same panel.

4. **Set the public bin ID in `index.html`**  
   - Open `index.html` in a text editor.  
   - Find the line:  
     ```js
     const PUBLIC_BIN_ID = "your_bin_id_here";
