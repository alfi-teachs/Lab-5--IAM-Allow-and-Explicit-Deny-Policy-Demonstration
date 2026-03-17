# Lab-5-IAM-Allow-and-Explicit-Deny-Policy-Demonstration
[
https://www.youtube.com/watch?v=QkISYZdU-DI&t=29s

# Part 1: Create IAM User (No Permissions)

Log in to AWS (root user)

Go to IAM (Identity and Access Management)

Click Users → Create user

User Setup

Enter username (example: test-user)

Enable:
✅ Console access

Set password (auto or custom)

Tick:
✅ User must create a new password at next sign-in

👉 Click Next → Skip permissions → Create user

# Part 2: Login as User (No Access)

Open Incognito window

Login using IAM user credentials

What you observe:

Cannot access S3

Cannot access IAM

Shows Access Denied

👉 This is because: No policy attached

# Part 3: Give Full Access (Allow Policy)

Now switch back to root/admin

Go to IAM → Users

Select test-user

Go to Permissions tab

Click Add permissions

Attach Full Access

Select:
✅ Attach policies directly

Search and select:
✅ AdministratorAccess (full access to all services)

👉 Click Next → Add permissions

# Part 4: Verify Full Access

Go back to Incognito window

Refresh or login again

Now you’ll see:

User can access S3

User can access IAM

Can create, delete, modify resources

👉 This proves: Allow policy gives permissions

# Part 5: Apply Explicit Deny Policy

Now we override access using Deny.

Go back to root/admin

Open IAM → Users

Select test-user

Create Inline Policy (Deny IAM Access)

Go to Permissions tab

Click Add permissions

Click:
✅ Create inline policy

JSON Policy

Paste this:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "iam:*",
      "Resource": "*"
    }
  ]
}

👉 Click Next

Name: iam-deny

👉 Click Create policy

# Part 6: Verify Deny in User Account

Go back to Incognito window

Refresh or login again

What You’ll See Now

IAM access → ❌ Denied

Even though user has AdministratorAccess

Cannot:

Create users

Delete users

View IAM

But:

Other services (like S3) may still work

Core Concept (Very Important)

Here’s the key rule in AWS:

✅ Allow gives access

❌ Explicit Deny always overrides Allow

What this really means:

Even if user has full access, a Deny policy will block it.

# Final Result

Initially: No access

After Allow: Full access

After Deny: IAM access blocked
