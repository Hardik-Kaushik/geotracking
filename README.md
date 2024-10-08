# geotracking
Geotracking and Internal Navigation Application

Project Overview: 
This project is an Express.js application with role-based authentication and live geotracking functionality. It allows users to interact with geofences and navigate through multiple floors of a building, while also tracking their live location within defined geofences. The geotracking system is built using Leaflet.js, and users can create custom polygons and circles as geofences, with real-time location tracking.

Folder Structure
├── middleware
│   └── auth.js          # Authentication middleware for handling user sessions and access control
├── models
│   └── location.js      # Location model schema for storing and managing location data
├── node_modules         # Node.js dependencies
├── public               # Static assets like images, CSS, and client-side JS files
├── src
│   └── config.js        # Configuration for environment variables and database connections
├── views
│   ├── admin.ejs        # Admin panel for managing users and system configurations
│   ├── geotracking.ejs  # Main page for live geotracking with geofence creation and management
│   ├── home.ejs         # Home page with basic information and navigation links
│   ├── internal-navigation.ejs  # Internal navigation page for floor-based geofence management
│   ├── login.ejs        # User login page with authentication features
│   ├── results.ejs      # Results page showing geotracking statistics such as enter/exit counts
│   └── signup.ejs       # User signup page with registration functionality
├── app.js               # Main server file that configures routes and middleware
├── package.json         # Dependencies and project metadata
├── package-lock.json    # Lock file for dependencies
└── README.md            # Project documentation

*-User Authentication in the Geotracking and Internal Navigation Application: 

The application uses role-based authentication to manage user access to various features. The authentication system ensures that only authorized users can access specific pages like the geotracking dashboard, internal navigation, or the admin panel.

Key Components:
*Authentication Middleware (auth.js): This middleware handles session management, verifies user credentials, and restricts access based on user roles (e.g., admin, user).
*Role-Based Access Control (RBAC): Different roles have different levels of access. For example:
*Admin: Can access the admin dashboard and manage users and geofences.
*User: Can access the geotracking and internal navigation functionalities but not the admin panel.

Authentication Workflow:
*Signup (signup.ejs):

Users register by providing their credentials (username, password, and other details).
User data is securely stored in the database using hashing for passwords (e.g., using bcrypt).

*Login (login.ejs):

Users log in by submitting their credentials.
The server checks the submitted credentials against the stored hashed passwords.
Upon successful authentication, a session is created, and the user is redirected to the appropriate dashboard based on their role.

*Session Management:

Once a user logs in, a session token (often stored as a cookie) is created. This token is used to keep track of the user’s session across different pages.
Session Expiration: Sessions may have a time limit, after which users are required to log in again.

*Protected Routes:

Certain routes are protected using the authentication middleware. The middleware checks if the user has a valid session and the correct role before granting access.
For example:
Only authenticated users can access the geotracking.ejs and internal-navigation.ejs pages.
Only admins can access the admin.ejs panel.

Security Measures:
*Password Hashing: Passwords are never stored as plain text in the database. Instead, a hashing algorithm like bcrypt is used to hash the passwords before storing them.
*Session Tokens: After login, session tokens are created and securely stored (usually in cookies). These tokens ensure that user sessions are maintained securely during navigation.
*HTTPS: To protect the communication between users and the server, the application should use HTTPS to prevent man-in-the-middle (MITM) attacks.
*Input Validation and Sanitization: User inputs (such as login credentials) are validated and sanitized to prevent common security vulnerabilities like SQL Injection or XSS (Cross-Site Scripting).

*-Geotracking Features (geotracking.ejs)

The geotracking.ejs file provides the functionality for live geolocation tracking and geofence management. The core features include:

*Map Initialization: The map is initialized using Leaflet.js with OpenStreetMap, Google Streets, and Google Satellite layers.

*Geofence Creation: Users can draw custom polygons and circles on the map to create geofences.

*Live Location Tracking: The user's real-time location is tracked, and their position is updated every 2 seconds.

*Geofence Entry and Exit Detection: The system detects when a user enters or exits a geofence (either polygon or circle) and provides notifications.

*Zoom Controls: A zoom slider allows users to adjust the map zoom level between 5 and 15.

*Start/Stop Tracking: Users can start and stop live geolocation tracking, and the results (entry/exit counts, elapsed time) are displayed on the results page.

*Backend Integration: The current location (latitude, longitude) is sent to the server (/api/locations) to store location data in real-time.

Internal Navigation Features (internal-navigation.ejs)
The internal-navigation.ejs file manages the internal navigation within buildings using multiple floors. Users can:

*Floor-based Geofence Management: Users can switch between different floors of a building and manage subareas within each floor.

*Geofence Visibility: When a geofence is created for a floor, it remains visible across all floors, and users can navigate and draw new subareas within that geofence.

*Unified Control Bar: A single control bar is used to manage geofences and subareas across all floors without introducing extra UI elements.

*Persistent Data: Once a geofence or subarea is saved, it is stored and accessible when the user revisits that floor, ensuring continuity in navigation.

Future Considerations and Updates

1. Networking Enhancements for Real-Time Updates
WebSockets Integration: Implement WebSockets to allow real-time geolocation updates and live tracking data synchronization across multiple clients and devices. This would improve performance by reducing the delay in geolocation tracking and allow multiple users to view and manage the same geofences simultaneously.

Distributed Server System: If scaled, this application could benefit from a distributed system, using microservices architecture. Each component (e.g., location tracking, geofence management) could be a microservice, ensuring better performance, scalability, and fault tolerance.

2. 3D Space Integration for Enhanced Internal Navigation
3D Geofencing: Extend the current 2D floor-based navigation system into a 3D environment by incorporating a third dimension for height (z-axis). This will allow for more accurate modeling of real-world buildings, especially multi-level structures such as skyscrapers, shopping malls, or hospitals.

Solution: Use a 3D mapping library like CesiumJS or Three.js for integrating 3D geofences and improving user navigation across levels and subareas.
Impact: Users could visualize and interact with geofences in a fully immersive 3D environment, helping with more precise internal navigation in multi-story buildings.
Vertical Geofencing: Adding the ability to define geofences not just in a flat, horizontal plane but also vertically within a 3D model. This would allow users to define boundaries within complex structures that span multiple floors.

3D Models and Realistic Rendering: Importing 3D models of buildings into the system to provide a real-world feel for navigation. Users could walk through 3D spaces, with realistic floor transitions and geofencing over multiple stories.

3. Augmented Reality (AR) Navigation
Integrate AR to provide indoor navigation assistance using mobile devices. Users can navigate floors with AR overlays on their device, enhancing user experience in large buildings such as airports, malls, or hospitals.
AR markers could be placed at key points in the real world (e.g., doors, corridors), guiding users visually in 3D space.