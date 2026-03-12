# N8N AI Automation Workflows

Production-ready N8N automation workflows for small businesses powered by AI agents. Open-source, MIT licensed, and built for real-world deployment.

---

## 🚀 Featured Workflow

### Dental Clinic Appointment Admin System

A **complete AI-powered appointment management system** for dental clinics with phone integration, real-time scheduling, and automated patient communications.

**🎯 What it does:**
- **Automated Appointment Booking** — AI assistant schedules appointments via phone, checks availability, and confirms bookings
- **Smart Rescheduling** — Validates new time slots and updates records without double-booking
- **Instant Cancellations** — Removes appointments and sends confirmations automatically
- **Insurance Verification** — Real-time lookup of member IDs and insurance status  
- **Availability Search** — AI-generated free time slots considering working hours and existing appointments
- **Patient & Doctor Lookups** — Fetches and formats appointment lists, doctor schedules, and patient records

**📞 How it works:**
1. Phone call triggers webhook → Patient identified by phone number
2. Request routed through Switch node based on action type (book/reschedule/cancel/etc.)
3. Supabase database queried/updated with patient and appointment data
4. AI agent (GPT-4) calculates availability for complex scheduling
5. Webhook response sent back to phone system with confirmation

**🛠 Tech Stack:**
- **N8N** — Workflow automation engine
- **Supabase** — PostgreSQL database backend
- **OpenAI GPT-4** — AI availability calculation  
- **Webhook Integration** — Twilio/Retell AI phone system compatible
- **60+ Nodes** — Fully production-tested over 7 days of development

---

## 📂 Repository Structure

```
workflows/
├── dental-clinic-appointment-admin-system.json
└── (more workflows coming soon)
```

---

## ⚙️ Installation & Setup

### Prerequisites
- N8N instance (self-hosted or n8n.cloud)
- Supabase account with database
- OpenAI API key (for availability AI agent)
- Phone system with webhook support (Twilio, Retell AI, etc.)

### Quick Start

1. **Import Workflow**
   - Download `dental-clinic-appointment-admin-system.json`
   - In N8N: **Workflows** → **Import from File** → Select JSON

2. **Configure Supabase**
   - Create tables: `dentalpatients canada`, `dentalappointmentscanada`, `dentaldoctorscanada`, `dentalinsurance`
   - Add Supabase credentials in N8N credential manager
   - Update table IDs in all Supabase nodes

3. **Set Up Phone Integration**
   - Copy webhook URL from the `Webhook` node
   - Configure your phone system to POST requests to this URL
   - Map phone system variables to match workflow expected format

4. **Add OpenAI Credentials**
   - Go to `LLM Engine` node → Add OpenAI API credentials
   - Model: GPT-4o (recommended for accuracy)

5. **Test All Actions**
   - Book appointment
   - Reschedule appointment
   - Cancel appointment
   - Check insurance
   - Get availability
   - List appointments/doctors

---

## 🗄️ Database Schema

### Required Supabase Tables

**dentalpatients canada**
- `id` (uuid, primary key)
- `name` (text)
- `phonenumber` (text)
- `email` (text)
- `doctorid` (text)

**dentalappointmentscanada**
- `id` (uuid, primary key)
- `patientid` (uuid, foreign key)
- `doctorid` (text)
- `appointmentdate` (timestamp)
- `reason` (text)

**dentaldoctorscanada**
- `id` (uuid, primary key)
- `name` (text)
- `specialty` (text)

**dentalinsurance**
- `id` (uuid, primary key)
- `memberid` (text)
- `phonenumber` (text)
- `status` (text)

---

## 🎨 Customization

### Modify Working Hours
Edit the `Generate Availability With AI` node:
```
Working hours are from 8:00 AM to 5:00 PM except Saturdays and Sundays
```

### Change Appointment Duration
Update time slot logic in AI prompt:
```
Time slots are 60 min long → Change to your preferred duration
```

### Add New Actions
1. Add condition to `Switch` node
2. Create new Supabase query branch
3. Add webhook response node

---

## 🚦 Production Deployment

**Tested & Production-Ready:**
- ✅ 7 days of intensive development and testing
- ✅ Real Twilio phone call integration verified
- ✅ Live Supabase data operations confirmed
- ✅ Zero-error execution in production environment

**Performance:**
- Response time: < 2 seconds per request
- Concurrent requests supported
- Error handling for all edge cases

---

## 🤝 Contributing

This repository is built for the **Claude for Open Source** program and the broader N8N community.

**How to contribute:**
- Submit workflow improvements via Pull Request
- Report issues or bugs
- Share your own N8N automation workflows
- Suggest new features or use cases

---

## 📜 License

MIT License — Free to use, modify, and distribute.

---

## 🙏 Credits

**Developer:** Athar Shaikh  
**Built for:** Dental clinics, healthcare automation, and small business AI solutions  
**Development Time:** 7 days (14 hours/day)  
**Powered by:** N8N, Supabase, OpenAI

---

## 📧 Support

For questions, customizations, or professional implementations:
- **GitHub Issues:** [Open an issue](https://github.com/Athar167/n8n-ai-automation-workflows/issues)
- **Discussions:** Share your use cases and success stories

---

## 🌟 Star this repo if it helped you automate your business!

More workflows coming soon — real estate AI, legal automation, and e-commerce pipelines.
