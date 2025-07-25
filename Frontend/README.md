# Medical Laboratory Information System

A secure, HIPAA-compliant web application for managing medical laboratory information, including patient records, lab results, and secure image management.

## Features

- Role-based access control for lab technicians and doctors
- Secure patient record management
- End-to-end encrypted medical images using Diffie-Hellman key exchange
- JWT authentication with token refresh mechanism
- Responsive design for desktop and mobile use

## Security Features

### End-to-End Encryption with Diffie-Hellman

This application implements Diffie-Hellman key exchange to establish secure communication channels for sensitive medical images:

1. **Key Exchange Process**:

   - After a user logs in, their browser initiates a key exchange with the server
   - Parameters for DH exchange (p, g) are received along with the server's public key
   - The client generates its own key pair and sends its public key to the server
   - Both client and server independently compute the same shared secret
   - This shared secret is used to derive encryption keys

2. **Image Security**:

   - Images uploaded by lab technicians are encrypted on the server using the negotiated keys
   - Only authorized doctors with valid encryption keys can view decrypted images
   - Encryption keys are never directly transmitted over the network
   - Keys are refreshed periodically (every 60 minutes) and on token refresh

3. **Encryption Status**:
   - The application displays the current encryption status to users
   - Green badge: End-to-end encryption active
   - Gray badge: Standard encryption (fallback)

## Architecture

### Frontend

- React 19.1.0
- React Router DOM 7.5.2
- Context API for state management
- Node-forge for cryptographic operations

### Authentication Flow

1. User login with credentials
2. JWT token received and stored
3. Diffie-Hellman key exchange performed
4. Periodic token and key refresh

### Components

- **AuthContext**: Manages authentication state and token refresh
- **PatientContext**: Handles patient data operations and secure image retrieval
- **EncryptionStatus**: Reusable component to display encryption status
- **Layout**: Main application layout and navigation

## Installation & Setup

### Prerequisites

- Node.js 14.x or higher
- npm 6.x or higher

### Installation Steps

1. Clone the repository

   ```
   git clone https://github.com/your-organization/medical-lab-system.git
   cd medical-lab-system
   ```

2. Install dependencies

   ```
   npm install
   ```

3. Start the development server

   ```
   npm start
   ```

4. Access the application at `http://localhost:3000`

## Usage

### Lab Technician Role

1. Add new patients with medical images
2. The system automatically encrypts sensitive areas of images

### Doctor Role

1. Search for patients by ID
2. View patient information
3. Access securely decrypted medical images

## API Integration

The frontend communicates with a Django backend API:

- **Base URL**: `http://localhost:8000`
- **Authentication**: JWT tokens
- **Key Exchange Endpoints**:
  - `GET /api/auth/key-exchange/`: Initiates key exchange
  - `POST /api/auth/key-exchange/`: Completes key exchange
- **Patient Endpoints**:
  - `GET /api/patients/{id}/`: Retrieves patient information
  - `POST /api/patients/`: Creates a new patient

## Security Considerations

- Never store encryption keys in localStorage, only use sessionStorage
- Implement proper error handling to prevent information leakage
- Ensure all communication occurs over HTTPS
- Clear keys when the user logs out or when the session expires

## Development Notes

### Adding New Features

When implementing new features:

1. Update necessary context providers
2. Ensure proper authentication is maintained
3. For new data types requiring encryption, follow the pattern in PatientContext.js
4. Always validate input on both client and server

### Troubleshooting Common Issues

- **"BigInteger not defined"**: Check node-forge import
- **Key exchange failures**: Verify network connectivity and authentication
- **Images not decrypting**: Ensure key exchange was successful

## License

This project is proprietary and confidential. Unauthorized use is prohibited.
#   t e s t 
 
 
