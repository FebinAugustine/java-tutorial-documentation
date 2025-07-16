# Final Keyword

The final keyword in Java is a non-access modifier that signifies that something is unchangeable or cannot be extended/overridden. It's a powerful tool for ensuring immutability, design integrity, and security in your code, which is critical in industry-level applications.

### It can be applied to:

### final Variables:

Makes a variable a constant.

### final Methods:

Prevents a method from being overridden by subclasses.

### final Classes:

Prevents a class from being subclassed (inherited).

## 1. final Variables (Constants)

Explanation:
When applied to a variable, final means its value (for primitives) or the object it refers to (for reference types) cannot be changed once it has been initialized.

### Primitive final: The value cannot be changed.

```Java

final int MAX_RETRIES = 3; // MAX_RETRIES can only be 3.
// MAX_RETRIES = 5; // Compile-time error!
```

### Reference final:

The reference itself cannot be reassigned to point to a different object. However, the contents of the object that the reference points to can still be modified if the object itself is mutable.

```Java

final List<String> NAMES = new ArrayList<>();
NAMES.add("Alice"); // Allowed: modifying the object's content
// NAMES = new LinkedList<>(); // Compile-time error: cannot reassign the reference
```

### Industry-Level Example:

Financial Transaction Object Immutability

- In financial systems, transaction records are sacred. Once a transaction occurs, its details (ID, amount, timestamp, sender, receiver) should never change. final variables are fundamental for ensuring the immutability of such critical data.

```Java

import java.time.LocalDateTime;
import java.util.Objects;

public final class FinancialTransaction { // Class itself is final (see point 3)
	private final String transactionId; // Must be initialized once, cannot be changed
	private final double amount; // Must be initialized once, cannot be changed
	private final String currency; // Must be initialized once, cannot be changed
	private final String senderAccount;
	private final String receiverAccount;
	private final LocalDateTime timestamp;

    public FinancialTransaction(
		String transactionId,
		double amount,
		String currency,
		String senderAccount, String receiverAccount
	)
	{
		// Validation during construction is key for immutable objects
		if (transactionId == null || transactionId.isEmpty()) {
			throw new IllegalArgumentException("Transaction ID cannot be empty.");
		}
		if (amount <= 0) {
			throw new IllegalArgumentException("Amount must be positive.");
		}
		if (currency == null || currency.isEmpty()) {
			throw new IllegalArgumentException("Currency cannot be empty.");
		}
		this.transactionId = transactionId;
		this.amount = amount;
		this.currency = currency;
		this.senderAccount = senderAccount;
		this.receiverAccount = receiverAccount;
		this.timestamp = LocalDateTime.now(); // Timestamp is set at creation
    }

    // Getters for all fields (no setters, as the object is immutable)
    public String getTransactionId() { return transactionId; }
    public double getAmount() { return amount; }
    public String getCurrency() { return currency; }
    public String getSenderAccount() { return senderAccount; }
    public String getReceiverAccount() { return receiverAccount; }
    public LocalDateTime getTimestamp() { return timestamp; }

    @Override
    public String toString() {
        return "Transaction{" +
               "id='" + transactionId + '\'' +
               ", amount=" + amount +
               ", currency='" + currency + '\'' +
               ", from='" + senderAccount + '\'' +
               ", to='" + receiverAccount + '\'' +
               ", time=" + timestamp +
               '}';
    }

    // A real immutable class would also override equals() and hashCode()
    @Override
    public boolean equals(Object o) {
		if (this == o) return true;
		if (o == null || getClass() != o.getClass()) return false;
		FinancialTransaction that = (FinancialTransaction) o;
		return Double.compare(that.amount, amount) == 0 &&
			Objects.equals(transactionId, that.transactionId) &&
			Objects.equals(currency, that.currency) &&
			Objects.equals(senderAccount, that.senderAccount) &&
			Objects.equals(receiverAccount, that.receiverAccount) &&
			Objects.equals(timestamp, that.timestamp);
	}

    @Override
    public int hashCode() {
		return Objects.hash(transactionId, amount, currency, senderAccount, receiverAccount, timestamp);
	}

}

public class TransactionProcessor {
public static void main(String[] args) {
// Once created, the FinancialTransaction object's state cannot be altered.
FinancialTransaction tx1 = new FinancialTransaction(
"TXN001", 100.50, "USD", "ACC123", "ACC456"
);

        System.out.println(tx1);

        // Attempting to change tx1.amount = 200.00; // This would be a compile-time error!
        // Attempting to change tx1.timestamp = LocalDateTime.now(); // Compile-time error!

        // If you need a modified transaction, you create a *new* one (e.g., for refunds or adjustments)
        // This ensures the original transaction record remains untouched.
        FinancialTransaction refundTx = new FinancialTransaction(
            "REF001", 100.50, "USD", "ACC456", "ACC123"
        );
        System.out.println(refundTx);
    }

}
```

### Benefit:

Guarantees that sensitive data, once set, cannot be accidentally or maliciously changed. This is vital for audit trails, consistency, and preventing bugs related to mutable state.

## 2. final Methods

Explanation:
When a method is declared final, it cannot be overridden by any subclass. This ensures that the implementation of that method remains consistent across the entire class hierarchy.

### Industry-Level Example:

Security or Core Logic in an Authentication/Encryption Utility

- Consider a security utility class where certain algorithms or validation steps must never be altered by subclasses to prevent security vulnerabilities or incorrect behavior.

```Java

// SecurityBase.java
public abstract class SecurityBase { // Abstract class, designed to be extended

    // This method performs a critical, non-negotiable security check.
    // Making it final ensures no subclass can bypass or modify this check.
    public final boolean validateAuthenticationToken(String token) {
        if (token == null || token.isEmpty()) {
            System.out.println("Validation failed: Token is null or empty.");
            return false;
        }
        // Complex token validation logic (e.g., JWT signature verification, expiration, etc.)
        // This is a simplified representation.
        if (token.length() > 10 && token.contains(".")) {
            System.out.println("Validation successful for token: " + token.substring(0,5) + "...");
            return true;
        } else {
            System.out.println("Validation failed: Invalid token format.");
            return false;
        }
    }

    // Other methods that might be overridden by subclasses
    public abstract void logSecurityEvent(String event);

}

// OAuth2SecurityService.java (a subclass implementing specific logging)
public class OAuth2SecurityService extends SecurityBase {

    @Override
    public void logSecurityEvent(String event) {
        System.out.println("OAuth2 Security Log: " + event + " at " + LocalDateTime.now());
        // Specific logging implementation for OAuth2, e.g., send to an audit service
    }

    public void processOAuthToken(String token) {
        // We rely on the final validateAuthenticationToken() method here.
        // It cannot be overridden by OAuth2SecurityService, ensuring its integrity.
        if (validateAuthenticationToken(token)) {
            System.out.println("Token is valid. Proceeding with OAuth2 authorization.");
            logSecurityEvent("Token validation success.");
        } else {
            System.out.println("Token is invalid. OAuth2 authorization failed.");
            logSecurityEvent("Token validation failure.");
        }
    }

}

public class SecurityManager {
public static void main(String[] args) {
OAuth2SecurityService authService = new OAuth2SecurityService();

        // The validateAuthenticationToken method is called, and its exact implementation
        // from SecurityBase is used. It cannot be changed by OAuth2SecurityService.
        authService.processOAuthToken("valid.jwt.token");
        System.out.println("---");
        authService.processOAuthToken("short_token");
        System.out.println("---");
        authService.processOAuthToken(null);

        // Attempting to override validateAuthenticationToken in OAuth2SecurityService
        // would result in a compile-time error:
        /*
        public class AttackerService extends SecurityBase {
            @Override
            public boolean validateAuthenticationToken(String token) { // Error! Cannot override final method
                return true; // Bypass security!
            }
            @Override
            public void logSecurityEvent(String event) {}
        }
        */
    }

}
```

### Benefit:

Guarantees that critical algorithms, security checks, or fundamental behaviors remain consistent and cannot be altered by future extensions of the class hierarchy. This maintains the integrity of core logic.

## 3. final Classes

#### Explanation:

When a class is declared final, it cannot be subclassed (extended). This means no other class can inherit from it.

### Industry-Level Example:

Immutable Value Objects or Security Critical Classes

### java.lang.String:

The String class itself is a prime example of a final class. Its immutability is crucial for security (e.g., in password handling, network protocols) and performance (string pooling).

- Core Configuration or Security Contexts: Classes that represent essential, unchangeable configurations or security contexts.
  Let's use a ConfigurationEntry that, once loaded, should be guaranteed to be the exact instance you expect, without any altered behavior from subclasses.

```Java

// ConfigurationEntry.java
// This class is final to ensure that its behavior and immutability are guaranteed.
public final class ConfigurationEntry {

	private final String key;
	private final String value;
	private final boolean isSensitive;

    public ConfigurationEntry(String key, String value, boolean isSensitive) {
        if (key == null || key.isEmpty()) {
            throw new IllegalArgumentException("Config key cannot be empty.");
        }
        // Value can be null/empty depending on requirements
        this.key = key;
        this.value = value;
        this.isSensitive = isSensitive;
    }

    public String getKey() { return key; }
    public String getValue() {
        if (isSensitive) {
            return "[REDACTED]"; // Example of internal logic
        }
        return value;
    }
    public boolean isSensitive() { return isSensitive; }

    @Override
    public String toString() {
        return "ConfigEntry{" +
               "key='" + key + '\'' +
               ", value='" + (isSensitive ? "[SENSITIVE]" : value) + '\'' +
               ", sensitive=" + isSensitive +
               '}';
    }

}

public class AppConfigLoader {
public static void main(String[] args) {
	// Create configuration entries
	ConfigurationEntry dbHost = new ConfigurationEntry("db.host", "localhost", false);
	ConfigurationEntry apiKey = new ConfigurationEntry("api.key", "super-secret-api-key-123", true);

    System.out.println(dbHost);
    System.out.println(apiKey);
    System.out.println("API Key value (should be redacted): " + apiKey.getValue());


    // Attempting to extend ConfigurationEntry would result in a compile-time error:
    /*
		class MaliciousConfigEntry extends ConfigurationEntry { // Error! Cannot inherit from final class

			public MaliciousConfigEntry(String key, String value, boolean isSensitive)
			{
				super(key, value, isSensitive);
			}
			// Could try to override getValue() to expose sensitive data
			// Or add new methods to bypass checks
    	}
    */
}
```

### Benefit:

Prevents unintended or malicious subclassing that could alter the class's behavior, break its contract, or introduce security vulnerabilities. It's often used for immutable value objects or core framework classes whose integrity is paramount.

**In summary,** the final keyword is a fundamental tool in Java for enforcing design decisions related to immutability, behavior consistency, and security, making applications more robust and predictable in real-world scenarios.

# Object Class

We learned every class in java extend an object class. <br>

So when we try to print an obj it will give us an output something like this: ClassName@7ad042f3.
To override this create a method called toString, which is available in the parent Object class.

```Java
Class Laptop
{
String model;
int price;
	// Overrides the Object method toString() which converts the whole value to a hash code
	public String toString() {
		return model + “ : “ price;
}
// checks the equality of two object. Overriding the parent method.
// these with IDE provided method creation.
public boolean equals(Laptop that) {
		if (this.model.equals(that.model) && this.price == that.price)
		{
 			return true;
		}
		else
			return false;
}

}

Laptop l1 = new Laptop();
Laptop l2 = new Laptop();

System.out.println(l1.equals(l2));


```
