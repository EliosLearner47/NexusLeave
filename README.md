<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NexusLeave Enterprise DBMS - Full-Stack Leave Management</title>
  <!-- Google Fonts & Lucide Icons -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest"></script>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <!-- App Header -->
  <header class="app-header">
    <div class="brand-container">
      <div class="brand-logo">
        <i data-lucide="calendar-check-2"></i>
      </div>
      <div>
        <div style="display: flex; align-items: center; gap: 8px;">
          <span class="brand-title">NexusLeave</span>
          <span class="brand-tag">Full-Stack DBMS v3.0</span>
        </div>
        <div style="font-size: 0.72rem; color: var(--text-muted);">Smart Workforce Attendance & Leave Platform</div>
      </div>
    </div>
    <div class="header-actions">
      <!-- Role Switcher -->
      <div class="role-switcher-card">
        <span class="role-switcher-label"><i data-lucide="users" style="width: 14px; height: 14px; vertical-align: middle;"></i> Switch Context:</span>
        <select id="role-select" class="role-select">
          <!-- Populated by JS -->
        </select>
      </div>
      <!-- User Profile Badge -->
      <div id="user-profile-badge" class="user-profile-badge">
        <!-- Populated by JS -->
      </div>
      <!-- Reset Data Button -->
      <button id="btn-reset-data" class="btn-reset" title="Reset DBMS Database to default seed state">
        <i data-lucide="rotate-ccw" style="width: 14px; height: 14px;"></i> Reset DBMS
      </button>
    </div>
  </header>
  <!-- Main Container -->
  <main class="app-container">
    <!-- View Navigation Tabs -->
    <div class="view-nav">
      <div class="nav-tabs">
        <button id="tab-employee" class="nav-tab active">
          <i data-lucide="user-check"></i> Employee Workspace
        </button>
        <button id="tab-admin" class="nav-tab">
          <i data-lucide="shield-alert"></i> Admin Approval Center
          <span id="pending-badge-count" class="badge-count">0</span>
        </button>
        <button id="tab-holidays" class="nav-tab">
          <i data-lucide="calendar"></i> Holidays & Audit Logs
        </button>
      </div>
      <button id="btn-open-apply-modal" class="btn-primary">
        <i data-lucide="plus-circle"></i> Apply For Leave
      </button>
    </div>
    <!-- ================= EMPLOYEE VIEW ================= -->
    <section id="view-employee-section">
      <!-- KPI Cards: Employee Balances -->
      <div id="employee-kpi-grid" class="kpi-grid">
        <!-- Populated by JS -->
      </div>
      <!-- Employee My Requests Section -->
      <div class="glass-card">
        <div class="section-header">
          <h2 class="section-title">
            <i data-lucide="file-text" style="color: var(--accent-primary);"></i> My Leave Applications
          </h2>
          <div class="filter-bar">
            <select id="employee-status-filter" class="select-filter">
              <option value="ALL">All Statuses</option>
              <option value="Pending">Pending</option>
              <option value="Approved">Approved</option>
              <option value="Rejected">Rejected</option>
              <option value="Cancelled">Cancelled</option>
            </select>
            <input type="text" id="employee-search-input" class="search-input" placeholder="Search reason or dates...">
          </div>
        </div>
        <div class="table-wrapper">
          <table class="data-table">
            <thead>
              <tr>
                <th>Request ID</th>
                <th>Leave Type</th>
                <th>Dates & Duration</th>
                <th>Reason</th>
                <th>Submitted On</th>
                <th>Status</th>
                <th>Review Details</th>
                <th>Actions</th>
              </tr>
            </thead>
            <tbody id="employee-requests-tbody">
              <!-- Populated by JS -->
            </tbody>
          </table>
        </div>
      </div>
    </section>
    <!-- ================= ADMIN VIEW ================= -->
    <section id="view-admin-section" style="display: none;">
      <!-- KPI Cards: Admin Overview -->
      <div id="admin-kpi-grid" class="kpi-grid">
        <!-- Populated by JS -->
      </div>
      <!-- Pending Approval Queue -->
      <div class="glass-card" style="border-left: 4px solid var(--status-pending);">
        <div class="section-header">
          <h2 class="section-title" style="color: var(--status-pending);">
            <i data-lucide="clock"></i> Pending Approval Queue
          </h2>
          <span style="font-size: 0.8rem; color: var(--text-muted);">Requires Manager Action</span>
        </div>
        <div class="table-wrapper">
          <table class="data-table">
            <thead>
              <tr>
                <th>Request ID</th>
                <th>Employee</th>
                <th>Department</th>
                <th>Leave Type</th>
                <th>Dates & Duration</th>
                <th>Reason & Emergency Contact</th>
                <th>Submitted</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="admin-pending-tbody">
              <!-- Populated by JS -->
            </tbody>
          </table>
        </div>
      </div>
      <!-- All Company Requests Directory -->
      <div class="glass-card">
        <div class="section-header">
          <h2 class="section-title">
            <i data-lucide="layers" style="color: var(--accent-secondary);"></i> Company Leave Directory
          </h2>
          <div class="filter-bar">
            <select id="admin-dept-filter" class="select-filter">
              <option value="ALL">All Departments</option>
            </select>
            <select id="admin-type-filter" class="select-filter">
              <option value="ALL">All Leave Types</option>
            </select>
            <select id="admin-status-filter" class="select-filter">
              <option value="ALL">All Statuses</option>
              <option value="Pending">Pending</option>
              <option value="Approved">Approved</option>
              <option value="Rejected">Rejected</option>
              <option value="Cancelled">Cancelled</option>
            </select>
            <input type="text" id="admin-search-input" class="search-input" placeholder="Search employee or keyword...">
          </div>
        </div>
        <div class="table-wrapper">
          <table class="data-table">
            <thead>
              <tr>
                <th>Request ID</th>
                <th>Employee</th>
                <th>Leave Type</th>
                <th>Duration</th>
                <th>Reason</th>
                <th>Status</th>
                <th>Reviewer Notes</th>
              </tr>
            </thead>
            <tbody id="admin-directory-tbody">
              <!-- Populated by JS -->
            </tbody>
          </table>
        </div>
      </div>
      <!-- Employee Quota Overview -->
      <div class="glass-card">
        <div class="section-header">
          <h2 class="section-title">
            <i data-lucide="users" style="color: #a855f7;"></i> Employee Leave Balance Summary
          </h2>
        </div>
        <div class="table-wrapper">
          <table class="data-table">
            <thead>
              <tr>
                <th>Employee</th>
                <th>Department</th>
                <th>Paid Leave (Used / Total)</th>
                <th>Sick Leave (Used / Total)</th>
                <th>Casual Leave (Used / Total)</th>
                <th>WFH Days (Used / Total)</th>
              </tr>
            </thead>
            <tbody id="admin-balances-tbody">
              <!-- Populated by JS -->
            </tbody>
          </table>
        </div>
      </div>
    </section>
    <!-- ================= HOLIDAYS & AUDIT VIEW ================= -->
    <section id="view-holidays-section" style="display: none;">
      <!-- Company Holidays Grid -->
      <div class="glass-card">
        <div class="section-header">
          <h2 class="section-title">
            <i data-lucide="sparkles" style="color: #f59e0b;"></i> Upcoming Company Holidays
          </h2>
        </div>
        <div id="holidays-grid" class="holiday-grid">
          <!-- Populated by JS -->
        </div>
      </div>
      <!-- System Audit Logs -->
      <div class="glass-card">
        <div class="section-header">
          <h2 class="section-title">
            <i data-lucide="history" style="color: var(--accent-primary);"></i> System Audit Log History
          </h2>
        </div>
        <div class="table-wrapper">
          <table class="data-table">
            <thead>
              <tr>
                <th>Timestamp</th>
                <th>User Context</th>
                <th>Action Event</th>
                <th>Details</th>
              </tr>
            </thead>
            <tbody id="audit-logs-tbody">
              <!-- Populated by JS -->
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </main>
  <!-- ================= MODALS ================= -->
  <!-- 1. Apply Leave Modal -->
  <div id="modal-apply-leave" class="modal-overlay">
    <div class="modal-container">
      <div class="modal-header">
        <h3 class="modal-title">
          <i data-lucide="calendar-plus" style="color: var(--accent-primary);"></i> Apply for Leave
        </h3>
        <button class="modal-close modal-close-btn">&times;</button>
      </div>
      <form id="form-apply-leave">
        <div class="form-group">
          <label class="form-label" for="apply-leave-type">Leave Category *</label>
          <select id="apply-leave-type" class="form-control" required>
            <!-- Populated by JS -->
          </select>
        </div>
        <div class="form-group">
          <label class="form-checkbox-label">
            <input type="checkbox" id="apply-is-halfday"> Is Half-Day Leave?
          </label>
        </div>
        <div id="halfday-options-container" class="form-group" style="display: none;">
          <label class="form-label">Half-Day Session *</label>
          <select id="apply-halfday-type" class="form-control">
            <option value="First Half (Morning)">First Half (Morning Session)</option>
            <option value="Second Half (Afternoon)">Second Half (Afternoon Session)</option>
          </select>
        </div>
        <div class="form-row">
          <div class="form-group">
            <label class="form-label" for="apply-start-date">Start Date *</label>
            <input type="date" id="apply-start-date" class="form-control" required>
          </div>
          <div class="form-group" id="end-date-group">
            <label class="form-label" for="apply-end-date">End Date *</label>
            <input type="date" id="apply-end-date" class="form-control" required>
          </div>
        </div>
        <!-- Calculated Duration Alert -->
        <div id="calculated-duration-alert" style="background: rgba(99, 102, 241, 0.15); border: 1px solid rgba(99, 102, 241, 0.3); padding: 10px 14px; border-radius: var(--radius-md); font-size: 0.85rem; margin-bottom: 1.25rem; display: flex; align-items: center; justify-content: space-between;">
          <span style="color: #a5b4fc; font-weight: 600;">Calculated Duration:</span>
          <span id="calculated-days-value" style="font-weight: 800; color: #ffffff;">0 Working Days</span>
        </div>
        <div class="form-group">
          <label class="form-label" for="apply-reason">Reason for Leave *</label>
          <textarea id="apply-reason" class="form-control" rows="3" placeholder="Provide clear reason for HR & Manager review..." required></textarea>
        </div>
        <div class="form-group">
          <label class="form-label" for="apply-emergency">Emergency Contact Phone</label>
          <input type="tel" id="apply-emergency" class="form-control" placeholder="+1 (555) 000-0000">
        </div>
        <div class="modal-footer">
          <button type="button" class="btn-secondary modal-close-btn">Cancel</button>
          <button type="submit" class="btn-primary">
            <i data-lucide="send"></i> Submit Application
          </button>
        </div>
      </form>
    </div>
  </div>
  <!-- 2. Reject Request Modal -->
  <div id="modal-reject-leave" class="modal-overlay">
    <div class="modal-container" style="border-top: 4px solid var(--status-rejected);">
      <div class="modal-header">
        <h3 class="modal-title" style="color: var(--status-rejected);">
          <i data-lucide="x-circle"></i> Reject Leave Request
        </h3>
        <button class="modal-close modal-close-btn">&times;</button>
      </div>
      <form id="form-reject-leave">
        <input type="hidden" id="reject-request-id">
        
        <div id="reject-summary-card" style="background: rgba(239, 68, 68, 0.1); border: 1px solid rgba(239, 68, 68, 0.2); padding: 12px; border-radius: var(--radius-md); margin-bottom: 1.25rem; font-size: 0.85rem;">
          <!-- Populated by JS -->
        </div>
        <div class="form-group">
          <label class="form-label" for="reject-reason">Rejection Reason / Manager Feedback *</label>
          <textarea id="reject-reason" class="form-control" rows="4" placeholder="Explain clearly why this leave application is rejected..." required></textarea>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn-secondary modal-close-btn">Cancel</button>
          <button type="submit" class="btn-primary" style="background: var(--status-rejected); box-shadow: 0 4px 15px rgba(239, 68, 68, 0.4);">
            <i data-lucide="x"></i> Confirm Rejection
          </button>
        </div>
      </form>
    </div>
  </div>
  <!-- Toast Notification Container -->
  <div id="toast-container" class="toast-container"></div>
  <!-- Full-Stack API Scripts -->
  <script src="js/api.js"></script>
  <script src="js/app.js"></script>
</body>
</html>
