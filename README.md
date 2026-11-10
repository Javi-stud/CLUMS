# Computer Laboratory User Monitoring System (CLUMS)

## Project Overview

The **Computer Laboratory User Monitoring System (CLUMS)** is a centralized computer monitoring system designed to automatically record and monitor user activities across computers in a computer laboratory.

The system records student login and logout activities, application usage, system shutdowns, restarts, and unexpected disconnections. It uses a monitoring agent installed on each laboratory computer to collect activity records and transmit them to a centralized server.

Administrators can access a centralized dashboard to monitor computer availability, view student sessions, review application usage, and track disconnection records.

The primary goal of CLUMS is to provide an automated, reliable, and centralized approach to managing and monitoring computer laboratory usage.

## Objectives

- Automate the recording of student computer usage.
- Monitor login, logout, shutdown, and restart activities.
- Track application usage during active sessions.
- Detect unexpected computer disconnections.
- Centralize monitoring records from all laboratory computers.
- Provide administrators with an organized monitoring dashboard.
- Maintain accurate historical records for reporting and auditing.

## Scope and Features

### 1. Centralized Computer Monitoring
- Register and manage laboratory computers.
- Monitor the connection status of each computer.
- Display computer information, including computer name, IP address, building, and room.
- Track the last communication time of each computer.

### 2. Student Login Monitoring
- Automatically detect student login activities.
- Record student identification and computer assignment.
- Track active student sessions.
- Maintain login history.

### 3. Application Usage Monitoring
- Detect applications currently being used.
- Record application start and end times.
- Calculate application usage duration.
- Associate application activity with the corresponding student session.

### 4. Login, Logout, and Shutdown Monitoring
- Record successful user logins.
- Detect user logout activities.
- Monitor system shutdowns and restarts.
- Maintain historical system activity records.

### 5. Unexpected Disconnection Detection
- Implement a heartbeat mechanism between monitoring agents and the central server.
- Detect computers that stop communicating with the server.
- Identify potentially unexpected disconnections.
- Record the last known active session and heartbeat.
- Detect computer reconnections.
- Classify disconnections as normal, unexpected, network-related, or unknown when evidence permits.

### 6. Monitoring Agent Management
- Register monitoring agents.
- Monitor agent connection status.
- Track agent versions and last communication.
- Identify inactive or unavailable agents.
- Configure monitoring intervals.

### 7. Centralized Administrator Dashboard
- Display overall laboratory computer status.
- View active student sessions.
- Review application usage records.
- Access login and logout history.
- View shutdown and restart records.
- Monitor unexpected disconnections.
- Generate monitoring reports.

## System Architecture

CLUMS follows a client-server architecture.

```text
       LABORATORY COMPUTERS
  ┌───────────────────────────┐
  │ Computer 01               │
  │ Monitoring Agent          │
  └─────────────┬─────────────┘
                │
  ┌─────────────▼─────────────┐
  │ Computer 02               │
  │ Monitoring Agent          │
  └─────────────┬─────────────┘
                │
  ┌─────────────▼─────────────┐
  │ Computer 03               │
  │ Monitoring Agent          │
  └─────────────┬─────────────┘
                │
                ▼
        CENTRAL SERVER
  ┌───────────────────────────┐
  │ Backend API               │
  │ Event Processor           │
  │ Heartbeat Monitor         │
  └─────────────┬─────────────┘
                │
                ▼
          DATABASE
  ┌───────────────────────────┐
  │ PostgreSQL                │
  │ Computer Records          │
  │ Student Sessions          │
  │ Application Usage         │
  │ Disconnection Logs        │
  └─────────────┬─────────────┘
                │
                ▼
     ADMINISTRATOR DASHBOARD
  ┌───────────────────────────┐
  │ Computer Monitoring       │
  │ Student Activity          │
  │ Reports and Analytics     │
  └───────────────────────────┘
```

### System Components

**Monitoring Agent**
- Installed on each laboratory computer.
- Collects system and user activity events.
- Monitors application usage.
- Sends periodic heartbeat messages.
- Communicates with the backend API.

**Backend Server**
- Receives monitoring events.
- Processes and validates incoming records.
- Manages computer and student sessions.
- Detects missing heartbeats.
- Provides data to the administrator dashboard.

**Database**
- Stores computer information.
- Maintains student session records.
- Stores application usage history.
- Records shutdown and disconnection events.

**Administrator Dashboard**
- Provides centralized access to monitoring information.
- Displays real-time computer statuses.
- Provides activity history and reports.

## Technology Stack

| Component | Technology |
|---|---|
| Monitoring Agent | Python / C# (.NET) |
| Operating System Monitoring | Windows Event Logs |
| Application Detection | Windows API / Process Monitoring |
| Backend | Node.js and Express.js |
| Database | PostgreSQL |
| Real-time Communication | WebSocket |
| Frontend | Flutter Web |
| Authentication | JWT |
| API Communication | REST API |

*The technology stack is the proposed development stack and may be adjusted during implementation.*

## Database Structure

The proposed database consists of the following main tables:

| Table | Description |
|---|---|
| computers | Stores laboratory computer information. |
| students | Stores student identification information. |
| user_sessions | Stores student login and logout records. |
| application_usage | Stores application usage history. |
| disconnection_logs | Stores computer disconnection records. |
| agent_heartbeats | Stores monitoring agent communication records. |
| administrators | Stores administrator accounts. |
| audit_logs | Stores administrative activities. |

## Unexpected Disconnection Detection

CLUMS uses a heartbeat mechanism to identify computers that stop communicating with the central server.

### Example Process

1. The monitoring agent sends a heartbeat every 10 seconds.
2. The server records the latest received heartbeat.
3. The server checks whether the computer continues sending heartbeats.
4. If no heartbeat is received within the configured timeout, the computer is marked as disconnected.
5. The system records the last known active session.
6. When the computer reconnects, the system updates its connection history.

### Disconnection Classification

| Type | Description |
|---|---|
| Normal Shutdown | Computer shuts down normally. |
| System Restart | Computer restarts. |
| User Logout | Student manually logs out. |
| Unexpected Disconnection | Computer stops communicating without a recorded normal shutdown. |
| Network Disconnection | Network communication is interrupted. |
| Unknown | Cause cannot be determined from available records. |

**Note:** A missing heartbeat alone cannot establish whether the computer lost power, the network failed, or the monitoring agent stopped working. Additional system events and available hardware monitoring can help identify the cause.

## Development Roadmap

Development will be divided into phases to ensure that each component is properly implemented and tested.

### Phase 1 – Backend and Database
- [ ] Set up the backend project.
- [ ] Configure PostgreSQL.
- [ ] Create database tables.
- [ ] Implement computer registration API.
- [ ] Implement student session API.
- [ ] Implement monitoring event API.

### Phase 2 – Monitoring Agent
- [ ] Develop the Windows monitoring agent.
- [ ] Implement login detection.
- [ ] Implement logout detection.
- [ ] Implement shutdown and restart detection.
- [ ] Implement application usage monitoring.
- [ ] Implement backend communication.

### Phase 3 – Heartbeat and Disconnection Detection
- [ ] Implement periodic heartbeat messages.
- [ ] Implement heartbeat timeout detection.
- [ ] Record unexpected disconnections.
- [ ] Implement reconnection detection.
- [ ] Implement event synchronization after reconnection.

### Phase 4 – Administrator Dashboard
- [ ] Develop the dashboard interface.
- [ ] Implement computer monitoring.
- [ ] Implement student session monitoring.
- [ ] Implement application usage monitoring.
- [ ] Implement disconnection history.
- [ ] Implement reports and analytics.

### Phase 5 – Integration and Testing
- [ ] Integrate monitoring agents with the backend.
- [ ] Test multiple laboratory computers.
- [ ] Test login and logout detection.
- [ ] Test shutdown and restart detection.
- [ ] Test unexpected disconnections.
- [ ] Test network interruptions and reconnections.
- [ ] Verify database record accuracy.

## Security and Privacy Considerations

- Require authenticated communication between monitoring agents and the backend.
- Implement role-based administrator access.
- Protect student information and monitoring records.
- Use secure communication protocols.
- Collect only information necessary for laboratory monitoring.
- Avoid collecting passwords, keystrokes, private document contents, or unrelated personal information.
- Inform students that laboratory computer activity is monitored.
- Maintain audit logs for administrative actions.

## Expected Outcome

Upon completion, CLUMS will provide a centralized platform that automatically monitors laboratory computers and records student usage activities.

The system is expected to help laboratory administrators:

- Monitor computer availability.
- Identify active and inactive laboratory computers.
- Track student computer usage.
- Review application usage history.
- Identify normal and unexpected disconnections.
- Maintain organized laboratory monitoring records.
- Generate reports for laboratory management.

## Project Status

**Development Stage:** Planning and Initial Development

CLUMS is intended to be developed incrementally, beginning with the backend, database, and Windows monitoring agent before proceeding to dashboard integration and system-wide testing.
