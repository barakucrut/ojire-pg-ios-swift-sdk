# Ojire Payment Gateway iOS SDK

SDK resmi Ojire Payment Gateway untuk iOS (SwiftUI) berbasis WKWebView.
Menggunakan **URL Journey** (success / pending / failed / close) sama seperti SDK React Native.

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

            onFailed: { data in
                print("❌ FAILED:", data)
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
| `id` | `String` | ✅ | Payment Intent ID |
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
| `onFailed` | `[String: Any]` | Payment gagal |
| `onClose` | `Void` | User menutup halaman pembayaran |

---

## Callback Data Example

```swift
[
  "status": "success",
  "transaction_id": "trx_123",
  "order_id": "order_456"
]
```

> Struktur data mengikuti query parameter dari URL redirect.

---

## Notes

- SDK otomatis disable cache (`WKWebsiteDataStore.nonPersistent`)
- JavaScript enabled secara default
- Alert JavaScript (`alert()`) akan tampil native di iOS
- Flow **INIT / READY handshake** otomatis

---

## License

MIT License  
© Ojire Payment Gateway
