# Security Specification for Personal Portfolio

## Data Invariants
- `pageContent` is a singleton document at `config/pageContent`.
- Stickers, customStickers, worldImages, and clickNotes are collections.
- Only the administrator (owner) should be able to create, update, or delete data.
- Public users can read all data to see the portfolio.

## The Dirty Dozen Payloads (to be rejected)
1. Unauthenticated write to `stickers`.
2. Unauthenticated write to `config/pageContent`.
3. Authenticated but non-admin write to `config/pageContent` (if we have an admin list).
4. Modification of `stickers` with extra illegal fields (Ghost Fields).
5. Setting extremely large strings for sticker text.
6. Injecting malicious types into scale or rotate fields.
7. Deleting the `pageContent` document.
8. Rapid-fire creation of thousands of stickers (size check).
9. Modifying `customStickers` to point to external URLs if only base64 is expected.
10. Spoofing `createdAt` timestamp.
11. Reading `private` data (none currently defined, but defaults should be deny).
12. Attempting to list all users (if users collection existed).

## Test Runner (Draft)
```typescript
// firestore.rules.test.ts (placeholder logic)
// - Verify read allowed for unauth.
// - Verify write denied for unauth.
// - Verify write allowed for admin.
```
