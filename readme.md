How to install SDK

## IOS Swift

> ⚠️ **Caution**
>
> You must get `customer_token`, `payment_secret` and `payment_id` first at your backend to OJIRE API via request to `/v1/payment-intents` endpoint

---

## Installation (Swift Package Manager)

Tambahkan dependency via **Xcode → Add Package Dependency**:

```
https://github.com/barakucrut/opg-test-sdk.git
```

---

## Basic Usage (SwiftUI)

```swift
import SwiftUI
import OjirePaySDK

struct ContentView: View {

    let intent: PaymentIntent

    var body: some View {
        OjireWebView(
            id: intent.id,
            clientSecret: intent.clientSecret,
            publicKey: "pk_xxx",
            token: intent.customerToken,
            envType: .sandbox,

            onSuccess: { data in
                print("✅ SUCCESS:", data)
            },

            onPending: { data in
                print("⏳ PENDING:", data)
            },

            onError: { data in
                print("❌ Error:", data)
            },

            onClose: {
                print("❎ CLOSED BY USER")
            }
        )
        .edgesIgnoringSafeArea(.all)
    }
}
```

---

## Props

| Name | Type | Required | Description |
|-----|-----|---------|-------------|
| `paymentId` | `String` | ✅ | Payment Intent ID |
| `clientSecret` | `String` | ✅ | Client secret dari backend |
| `publicKey` | `String` | ✅ | Public key merchant |
| `token` | `String` | ✅ | Customer token |
| `envType` | `OjireEnvType` | ❌ | Environment (`.sandbox` default) |

---

## Available Environment

```swift
public enum OjireEnvType {
    case dev
    case sandbox
    case prod
}
```

---

## Callbacks

| Callback | Params | Description |
|--------|-------|------------|
| `onSuccess` | `[String: Any]` | Payment sukses |
| `onPending` | `[String: Any]` | Payment pending |
| `onError` | `[String: Any]` | Payment gagal |
| `onClose` | `Void` | User menutup halaman pembayaran |

---


