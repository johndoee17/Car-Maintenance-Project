# Technical Evidence Checklist

Capture these screenshots while the application is running and place the strongest evidence in the Technical Document / video demonstration.

## Frontend evidence

- Registration screen
- Login screen
- Protected dashboard with real MongoDB totals
- Empty dashboard state for a new user
- Add Vehicle form
- Vehicle list
- Vehicle details
- Edit Vehicle form
- Delete Vehicle confirmation
- Add Service Record form
- Service history list
- Edit Service Record form
- Validation error state
- Empty service-history state

## Backend / API evidence

- Successful `POST /api/auth/register`
- Duplicate email rejected
- Successful `POST /api/auth/login`
- Protected endpoint rejected without token
- Successful vehicle create/list/update/delete
- Successful service create/list/update/delete
- Invalid negative mileage/cost rejected
- Cross-user vehicle access rejected
- Cross-user service access rejected

## Database evidence

- `users` collection showing password hash rather than plaintext password
- `vehicles` collection showing `owner` reference
- `servicerecords` collection showing `owner` and `vehicle` references
- Before/after evidence showing service records removed when their vehicle is deleted

## Code evidence for the video

Explain these files briefly:

1. `backend/src/middleware/auth.js` — token verification and authenticated user resolution
2. `backend/src/controllers/vehicleController.js` — owner-scoped CRUD and cascading service cleanup
3. `backend/src/controllers/serviceController.js` — service records restricted to the authenticated owner and a valid owned vehicle
4. `frontend/src/context/AuthContext.jsx` — frontend authentication state
5. `frontend/src/pages/VehicleDetails.jsx` — end-to-end service-history workflow
