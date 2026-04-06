# Features

## feat01 Popup Control

**Goal:**
Enable teacher to control popup interaction for participants.

**Behavior:**
- View controls popup navigation
- Popup syncs with view
- Supports forward/back

**Non-Goals:**
- No server sync required

**Decisions:**
- Use client-side messaging

---

## feat02 Question Navigation

**Goal:**
Allow users to navigate between questions.

**Behavior:**
- Next/Back buttons
- History preserved

**Non-Goals:**
- No random resets

**Decisions:**
- Maintain session state
