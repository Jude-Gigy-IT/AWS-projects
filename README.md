<h1>☁️ AWS Identity and Access Management (IAM) Security Lab</h1>

<h2>Overview</h2>
<p>
This project demonstrates the design and implementation of a secure AWS Identity and Access Management environment using IAM users, groups, policies, MFA, and CloudTrail auditing.
The goal was to simulate a small enterprise cloud environment where users receive only the permissions required for their role.
</p>

<h2>Objectives</h2>
<ul>
  <li>Implement role-based access control using IAM groups</li>
  <li>Apply the principle of least privilege</li>
  <li>Enable MFA for administrative access</li>
  <li>Validate permissions through access testing</li>
  <li>Use CloudTrail to audit IAM management activity</li>
</ul>

<h2>Technologies Used</h2>
<ul>
  <li>Amazon Web Services</li>
  <li>AWS IAM</li>
  <li>AWS CloudTrail</li>
</ul>

<h2>Lab Architecture</h2>
<p>
The lab used a single AWS account with multiple IAM users, groups, and managed policies.
CloudTrail was enabled to monitor and audit IAM-related management events.
</p>

<img src="architecture/aws-iam-architecture.png" alt="AWS IAM Architecture Diagram">

<h2>IAM User and Group Design</h2>

<table>
  <tr>
    <th>User</th>
    <th>Group</th>
    <th>Assigned Policy</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td>Admin</td>
    <td>Admins</td>
    <td>AdministratorAccess</td>
    <td>Administrative access to manage AWS resources</td>
  </tr>
  <tr>
    <td>Developer</td>
    <td>Developers</td>
    <td>AmazonEC2ReadOnlyAccess</td>
    <td>Read-only visibility into EC2 resources</td>
  </tr>
  <tr>
    <td>HR</td>
    <td>HR</td>
    <td>AmazonS3ReadOnlyAccess</td>
    <td>Read-only access to S3 resources</td>
  </tr>
  <tr>
    <td>Intern</td>
    <td>Interns</td>
    <td>ReadOnlyAccess</td>
    <td>Safe read-only access across AWS services</td>
  </tr>
</table>

<h3>IAM Users</h3>
<img src="screenshots/02-iam-users.png" alt="IAM Users">

<h3>IAM Groups</h3>
<img src="screenshots/03-iam-groups.png" alt="IAM Groups">

<h3>Developer Group Policy</h3>
<img src="screenshots/04-developer-group-policy.png" alt="Developer Group Policy">

<h2>Security Controls Implemented</h2>

<h3>Role-Based Access Control</h3>
<p>
Permissions were assigned through IAM groups instead of directly attaching policies to individual users.
This makes access management easier to scale and reduces the risk of inconsistent permissions.
</p>

<h3>Principle of Least Privilege</h3>
<p>
Each user was assigned only the permissions needed for their role.
For example, the Developer user could view EC2 resources but could not modify unrelated AWS services.
</p>

<h3>Multi-Factor Authentication</h3>
<p>
MFA was enabled for the administrative account to strengthen authentication security and reduce the risk of account compromise.
</p>

<img src="screenshots/05-mfa-enabled.png" alt="MFA Enabled">

<h2>Permission Validation</h2>

<h3>Access Denied Test</h3>
<p>
The Developer user attempted an action outside the permissions granted by the Developers group.
AWS denied the request, confirming that least privilege controls were working as expected.
</p>

<img src="screenshots/06-access-denied-developer.png" alt="Access Denied Developer Test">

<h3>Administrator Access Test</h3>
<p>
The Admin user successfully performed an administrative action, validating that the Admins group had the correct level of access.
</p>

<img src="screenshots/07-admin-success.png" alt="Administrator Success">

<h2>CloudTrail Auditing</h2>
<p>
CloudTrail was enabled to record AWS management events.
After creating a test IAM user, the <code>CreateUser</code> event appeared in CloudTrail Event History.
This demonstrated that IAM administrative actions were being logged for auditing and investigation.
</p>

<img src="screenshots/08-cloudtrail-event-history.png" alt="CloudTrail Event History">

<h3>CloudTrail Event Details</h3>
<img src="screenshots/09-cloudtrail-createuser-details.png" alt="CloudTrail CreateUser Event Details">

<h2>Lessons Learned</h2>
<ul>
  <li>IAM groups make permission management more scalable than assigning policies directly to users.</li>
  <li>Least privilege reduces risk by limiting unnecessary access.</li>
  <li>MFA is especially important for privileged accounts.</li>
  <li>CloudTrail provides visibility into administrative activity for auditing and incident response.</li>
  <li>Using an IAM administrator instead of the root account follows AWS security best practices.</li>
</ul>

<h2>Future Improvements</h2>
<ul>
  <li>Create custom IAM policies instead of relying only on AWS managed policies</li>
  <li>Add S3 bucket policy testing</li>
  <li>Enable GuardDuty for threat detection</li>
  <li>Integrate CloudTrail logs with a SIEM such as Wazuh</li>
  <li>Expand the lab into a broader AWS cloud security project</li>
</ul>
