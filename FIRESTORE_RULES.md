# Firestore Security Rules

## How to Update Firestore Rules

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: `bar-review-tracker`
3. Navigate to **Firestore Database** → **Rules** tab
4. Replace the existing rules with the rules below
5. Click **Publish**

## Recommended Security Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Reviews collection - allow authenticated users to read and write
    match /reviews/{reviewId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update: if request.auth != null;
      allow delete: if request.auth != null;
    }
    
    // Metadata collection - allow authenticated users to read and write
    match /metadata/{document=**} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
  }
}
```

## Notes

- These rules require users to be authenticated (logged in) to read/write
- All authenticated users can read and write to the reviews collection
- If you want to restrict access further, you can add additional conditions

## Testing

After updating the rules, try adding a review again. If you still get permission errors, check:
1. You are logged in (check the auth state)
2. The rules were published successfully
3. There are no syntax errors in the rules

