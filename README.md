# Hospital Management System (HMS)

A comprehensive Flask-based web application for managing hospital operations, including patient registration, doctor management, appointment scheduling, and treatment tracking.

## Features

### Patient Management
- **Registration & Login**: Secure patient registration and authentication
- **Dashboard**: View upcoming and past appointments
- **Appointment Booking**: Book appointments with available doctors
- **Doctor Search**: Search and filter doctors by specialization
- **Profile Management**: Edit personal information and contact details
- **Medical History**: View past appointments and treatments

### Doctor Management
- **Doctor Login**: Secure authentication for medical staff
- **Dashboard**: View today's and upcoming appointments
- **Availability Management**: Set weekly availability schedule
- **Patient History**: Access patient medical records
- **Treatment Recording**: Add diagnosis, prescription, and follow-up notes
- **Appointment Status**: Update appointment status (Booked, Completed, Cancelled)

### Admin Management
- **Admin Dashboard**: Overview of doctors, patients, and appointments
- **Doctor Management**: Add, edit, view, and delete doctors
- **Patient Management**: Add, edit, view, and manage patients
- **Appointment Tracking**: View all appointments and their status
- **Search Functionality**: Search for doctors and patients by various criteria

## Project Structure

```
MAD1-Project/
├── app.py                      # Main Flask application
├── db.py                        # Database initialization and setup
├── requirements.txt             # Python dependencies
├── models/                      # Data models and business logic
│   ├── __init__.py
│   ├── admin.py                # Admin-related functions
│   ├── patient.py              # Patient-related functions
│   ├── doctor.py               # Doctor-related functions
│   ├── appointment.py          # Appointment booking logic
│   └── tmt.py                  # Treatment-related functions
├── templates/                  # HTML templates
│   ├── index.html              # Home page
│   ├── patient_login.html
│   ├── patient_register.html
│   ├── patient_dashboard.html
│   ├── patient_edit.html
│   ├── patient_history.html
│   ├── doctor_login.html
│   ├── doctor_dashboard.html
│   ├── doctor_availability.html
│   ├── doctor_view_patient_history.html
│   ├── admin_login.html
│   ├── admin_dashboard.html
│   ├── admin_add_doctor.html
│   ├── admin_edit_doctor.html
│   ├── admin_view_doctor.html
│   ├── admin_search_doctor.html
│   ├── admin_edit_patient.html
│   ├── admin_view_patient.html
│   ├── admin_search_patient.html
│   └── admin_all_appointments.html
└── data/                       # Sample data files
    ├── admindata.py
    ├── doctordata.py
    ├── patientData.py
    ├── Appointdata.py
    └── Treatmentdata.py
```

## Technology Stack

- **Backend**: Python 3.x with Flask
- **Database**: SQLite3
- **Frontend**: HTML, CSS, JavaScript
- **Security**: Werkzeug (password hashing)
- **Authentication**: Flask Sessions

## Installation

### Prerequisites
- Python 3.7 or higher
- pip (Python package manager)

### Setup Steps

1. **Navigate to the project directory**:
   ```powershell
   cd "c:\Users\Utkarsh Singh\Desktop\HMS\HMS\MAD1-Project"
   ```

2. **Create a virtual environment** (recommended):
   ```powershell
   python -m venv venv
   .\venv\Scripts\Activate.ps1
   ```

3. **Install dependencies**:
   ```powershell
   pip install flask werkzeug
   ```
   
   Or if a `requirements.txt` exists:
   ```powershell
   pip install -r requirements.txt
   ```

4. **Initialize the database**:
   ```powershell
   python db.py
   ```
   
   This will create `hospital_mgmt.db` and populate it with initial data.

## Running the Application

```powershell
python app.py
```

The application will start on `http://127.0.0.1:5000`

Open your browser and navigate to the URL above.

## Default Credentials

### Admin Account
- **Email**: admin@hms.com
- **Password**: admin123

### Sample Patient
- **Email**: ashika@gmail.com
- **Mobile**: 9245678110

### Sample Doctor
- **Email**: dr.sulab@gmail.com
- **Mobile**: 9362170250

## Database Schema

### Tables

**Department**
- Dept_id (Primary Key)
- DeptName
- Description
- Doctors_Registered (Auto-updated via trigger)

**Doctor**
- doc_id (Primary Key)
- DName
- DMobileNumber (Unique)
- Email (Unique)
- Timings
- Dept_id (Foreign Key)

**Patient**
- patient_id (Primary Key)
- PName
- PMobileNumber (Unique)
- Email (Unique)
- Gender
- DOB
- Address
- Optional_Contact
- Blood_group

**Appointment**
- App_id (Primary Key, Auto-increment)
- patient_id (Foreign Key)
- doc_id (Foreign Key)
- Date
- Time
- status (Booked, Completed, Cancelled)

**Treatment**
- Tmt_id (Primary Key, Auto-increment)
- App_id (Foreign Key)
- Diagnosis
- prescription
- FollowUp
- Notes
- Cost

**Admin**
- id (Primary Key, Auto-increment)
- username (Unique)
- password (Hashed)
- name

## API Routes

### Patient Routes
- `GET /` - Home page
- `GET/POST /patient/register` - Patient registration
- `GET/POST /patient/login` - Patient login
- `GET /patient/dashboard` - Patient dashboard
- `POST /patient/book` - Book an appointment
- `GET /patient/cancel/<app_id>` - Cancel appointment
- `GET/POST /patient/edit` - Edit patient profile
- `GET /patient/departments` - View all departments
- `GET /patient/doctors` - View all doctors
- `GET /patient/search` - Search for doctors
- `GET /patient/history` - View patient medical history

### Doctor Routes
- `GET/POST /doctor/login` - Doctor login
- `GET /doctor/dashboard` - Doctor dashboard
- `POST /doctor/mark_status` - Update appointment status
- `POST /doctor/add_treatment` - Add treatment details
- `GET/POST /doctor/availability` - Manage availability
- `GET /doctor/patient_history/<patient_id>` - View patient details

### Admin Routes
- `GET/POST /admin/login` - Admin login
- `GET /admin/dashboard` - Admin dashboard
- `GET /admin/search_doctor` - Search doctors
- `GET /admin/search_patient` - Search patients
- `GET/POST /admin/add_doctor` - Add new doctor
- `GET/POST /admin/edit_doctor/<doctor_id>` - Edit doctor
- `GET /admin/view_doctor/<doctor_id>` - View doctor details
- `DELETE /admin/delete_doctor/<doctor_id>` - Delete doctor
- `GET/POST /admin/edit_patient/<patient_id>` - Edit patient
- `GET /admin/view_patient/<patient_id>` - View patient details
- `DELETE /admin/delete_patient/<patient_id>` - Delete/blacklist patient
- `GET /admin/all_appointments` - View all appointments

### Common Routes
- `GET /logout` - Logout user

## Features in Detail

### Session Management
The application uses Flask sessions to manage user authentication. Session keys:
- `patient_id` - Currently logged-in patient
- `doctor_id` - Currently logged-in doctor
- `admin` - Currently logged-in admin username

### Appointment Status
Appointments can have the following statuses:
- **Booked**: Initial appointment status
- **Completed**: Doctor has completed the appointment
- **Cancelled**: Patient or admin cancelled the appointment

### Security Features
- Password hashing using Werkzeug
- Session-based authentication
- Route protection with session checks
- CSRF protection via Flask sessions

## Troubleshooting

### Database Issues
- Delete `hospital_mgmt.db` and re-run `db.py` to reset the database
- Ensure SQLite3 is installed (usually comes with Python)

### Import Errors
- Verify all model files exist in the `models/` directory
- Ensure the database initialization completed successfully

### Port Already in Use
- If port 5000 is in use, modify the last line of `app.py`:
  ```python
  app.run(debug=True, port=5001)  # Change to different port
  ```

## Future Enhancements
- Email notifications for appointments
- SMS reminders
- Payment integration
- Advanced reporting and analytics
- Mobile app support
- Prescription PDF generation
- Appointment rescheduling
- Doctor availability calendar view

## License
This project is for educational purposes.

## Support
For issues or questions, contact the development team.
