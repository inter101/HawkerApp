# HawkerGo

A Flutter mobile app that digitalises ordering at Singapore hawker centres. Customers browse stalls, order food and track their orders in one place, instead of standing in long queues at mealtimes.

> Built as a group project for **ET0529** at Singapore Polytechnic (Diploma in Computer Engineering, DCPE/FT/2B/22).

## The problem

Hawker centres in Singapore get very crowded at mealtimes. People often queue in long, hot lines without knowing when their food will be ready. HawkerGo lets customers place orders from their phone and get notified when the food is ready, while stalls receive orders digitally.

## Features

**Customer app (implemented in this repository)**

- **Browse and search:** view stalls and their menus, and search for stalls or dishes
- **Popular dishes:** the home page highlights popular dishes that can be added to the cart straight away
- **Cart and checkout:** order summary with dine-in or takeaway options (takeaway adds a $0.50 fee)
- **Points and rewards:** earn 5 points per $1 spent, and redeem points as a discount at checkout (minimum 50 points; 1 point = $0.02)
- **Payment setup:** add a card, verified with a one-time password sent as an on-device notification (payment is simulated; no real payment gateway)
- **Order-ready notifications:** local push notifications when an order is ready
- **Order history:** view past and current orders, saved to Firestore so they persist across sessions
- **Ratings and reviews:** rate an order and leave a comment after checkout
- **Profile and support:** account settings, help and support, contact support and app feedback pages
- **Persistent login:** returning users are signed back in automatically

**Planned / in the project proposal**

The original proposal also covers a hawker-facing side. These are not part of the code in this repository:

- Hawker registration and login, stall info and open/closed status
- A dashboard showing revenue, orders completed and the live queue, with new-order alerts
- Menu management: add dishes with photos, delete dishes, mark items out of stock
- Daily order history with calendar date selection
- AI-generated daily performance summary (comparison with the average, best and worst sellers, summarised customer reviews)

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Flutter (Dart) |
| Database | Cloud Firestore |
| File storage | Firebase Storage |
| Notifications | `flutter_local_notifications` |
| Local storage | `shared_preferences` |

## Project structure

```
lib/
├── main.dart                 # App entry point, Firebase init, routes
├── homepage.dart             # Welcome screen
├── second_home.dart          # Customer home (popular dishes)
├── stall.dart                # Stalls list and search
├── stall_detail_page.dart    # Stall menu
├── cart.dart / cart_service.dart       # Cart, points, order history logic
├── checkout_page.dart        # Checkout and order summary
├── payment_setup_page.dart   # Card setup with OTP verification
├── history_page.dart         # Order history
├── rate_order_page.dart      # Ratings and reviews
├── customer_service.dart     # Customer accounts and login
├── notification_service.dart # Local notifications
└── profile_page.dart, account_settings_page.dart, help_support_page.dart, ...
```

## Getting started

### Prerequisites

- [Flutter SDK](https://docs.flutter.dev/get-started/install) (Dart SDK `^3.11.5`)
- Android Studio or VS Code with the Flutter extension
- A Firebase project with **Cloud Firestore** and **Storage** enabled

### Setup

1. Clone the repository
   ```bash
   git clone <your-repo-url>
   cd hawker_gooo
   ```
2. Install dependencies
   ```bash
   flutter pub get
   ```
3. Connect your own Firebase project
   ```bash
   dart pub global activate flutterfire_cli
   flutterfire configure
   ```
   This regenerates `lib/firebase_options.dart`. For Android, place your own `google-services.json` in `android/app/`.
4. Run the app
   ```bash
   flutter run
   ```

On first launch the app seeds two sample customer accounts if the `customers` collection is empty.

### Firestore collections used

`Hawker` (with `profile` and `Menu` sub-collections), `customers` (with `orderHistory`), `history`, `reviews`, `app_feedback`

## Known limitations

This is a student prototype, and some parts are simplified:

- Login is handled with a custom check against Firestore rather than Firebase Authentication, and passwords are not hashed. A production version should use Firebase Authentication.
- Payment is simulated. No real payment provider is integrated.
- Firestore security rules should be tightened before any real use.
