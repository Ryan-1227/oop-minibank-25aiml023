
**MiniBank** is an enterprise-grade, console-based banking application developed progressively across 14 laboratory sessions. It demonstrates core and advanced Object-Oriented Programming (OOP) paradigms in modern Java (JDK 17+), integrating:

- **Encapsulated Data Models & Records** (`BankInfo`, `Customer`, `Account`, `Command`)
- **Polymorphism & Class Hierarchies** (`SavingsAccount`, `CurrentAccount`, `FixedDepositAccount`)
- **Interfaces & Lambdas** (`Transactable`, `InterestBearing`, `WithdrawRule`, `Premium`)
- **Custom Metadata & Runtime Reflection** (`@Id`, `@Positive`, `@MaxLength`, `@Audit`, `AnnotationValidator`)
- **Robust Exception Hierarchies** (`BankException`, `InsufficientFundsException` with shortfall tracking)
- **Multi-threading & Thread Safety** (Race condition prevention via `synchronized` methods, `AccountWorker`)
- **Enterprise Concurrency Engine** (`TransactionProcessor`, `ExecutorService`, Deadlock Prevention via consistent lock ordering, Producer-Consumer buffer with `wait()` / `notify()`)
- **Object Serialization & NIO Log Processing** (`StatePersister`, `TransactionLog`, `ReportGenerator` with `DirectoryStream`)
- **Collections Framework & Sorting** (`HashMap`, `ArrayList`, `Comparator`, `Comparable`, `ConcurrentHashMap`)
- **Generic Data Access Layer** (`Repository<T>` with reflected `@Id` resolution, `@SafeVarargs`, bounded generic parameters `<N extends Number>`)
- **Layered Architecture & Comprehensive JUnit 5 Test Suite** (`BankService`, `MiniBankTest`)

---

## 📁 Project Structure

```
oop-minibank/
├── .gitignore                      # Git ignore file for binaries and runtime data
├── README.md                       # Comprehensive project documentation & viva guide
├── build.sh / build.bat            # Build automation script (compiles & packages JAR)
├── run.sh / run.bat                # Execution script
├── test.sh / test.bat              # JUnit 5 test execution script
├── minibank.jar                    # Final runnable application JAR
├── lib/
│   └── junit-platform-console-standalone.jar  # Zero-dependency JUnit 5 runner
├── src/
│   └── minibank/
│       ├── MiniBank.java           # Main interactive entry point & Lab Milestone Demo
│       ├── model/
│       │   ├── BankInfo.java       # Record for bank header info (Lab 1)
│       │   ├── MenuOption.java     # Navigation enum (Lab 1 & 14)
│       │   ├── TransactionType.java# Enum: DEPOSIT, WITHDRAW, TRANSFER (Lab 4)
│       │   ├── Command.java        # Record for parsed CLI commands (Lab 4)
│       │   ├── Customer.java       # Customer entity with static ID counter & clone() (Lab 2, 3, 11)
│       │   ├── Account.java        # Abstract base account (Lab 2, 3, 5, 6, 7, 8, 9, 11, 12)
│       │   ├── SavingsAccount.java # Savings account with minBalance & 4% interest (Lab 5)
│       │   ├── CurrentAccount.java # Current account with overdraft & 0% interest (Lab 5)
│       │   ├── FixedDepositAccount.java # FD account with 7% interest (Lab 5)
│       │   ├── Transactable.java   # Interface for deposit/withdraw (Lab 6)
│       │   ├── InterestBearing.java# Interface with default interest calculation (Lab 6)
│       │   ├── WithdrawRule.java   # @FunctionalInterface for lambda withdrawal rules (Lab 6, 7)
│       │   ├── Premium.java        # Marker interface (Lab 6)
│       │   └── annotation/
│       │       ├── Id.java         # @Id marker for entity keys (Lab 7, 13)
│       │       ├── Positive.java   # @Positive numeric validator (Lab 7)
│       │       ├── MaxLength.java  # @MaxLength string validator (Lab 7)
│       │       └── Audit.java      # @Audit reflective method annotation (Lab 14)
│       ├── exception/
│       │   ├── BankException.java  # Base checked exception (Lab 8)
│       │   ├── InsufficientFundsException.java # Carries shortfall amount (Lab 8)
│       │   ├── AccountNotFoundException.java   # Unknown account ID (Lab 8)
│       │   ├── InvalidAmountException.java     # Negative/zero amount error (Lab 8)
│       │   └── DailyLimitExceededException.java# Supplementary limit exception (Lab 8)
│       ├── repository/
│       │   ├── Repository.java     # Generic Repository<T> using reflection on @Id (Lab 13)
│       │   └── AccountStore.java   # Collections store with Comparator sorting (Lab 12)
│       ├── service/
│       │   ├── BankService.java    # Complete service layer facade (Lab 14)
│       │   ├── AuditLogger.java    # Reflective logger for @Audit methods (Lab 14)
│       │   ├── BankSession.java    # AutoCloseable session for try-with-resources (Lab 8)
│       │   ├── AccountWorker.java  # Runnable worker demonstrating concurrency (Lab 9)
│       │   └── TransactionProcessor.java # Managed thread pool & deadlock-free engine (Lab 10, 12)
│       └── util/
│           ├── Validator.java      # Regex validation (Mobile, Email, PAN, IFSC) (Lab 4)
│           ├── CommandParser.java  # CLI command tokeniser and parser (Lab 4)
│           ├── StatementFormatter.java # Multi-line StringBuilder statement builder (Lab 4)
│           ├── AnnotationValidator.java# Reflection validator for annotations (Lab 7)
│           ├── StatePersister.java # Object serialization save/load (Lab 11)
│           ├── TransactionLog.java # NIO append-only log recorder (Lab 11)
│           └── ReportGenerator.java# NIO DirectoryStream audit report generator (Lab 11)
├── test/
│   └── minibank/
│       └── MiniBankTest.java       # JUnit 5 test suite (Lab 14)
└── data/                           # Generated persistent state and transaction logs
    ├── accounts.dat
    └── logs/
```

---

## 🧭 Laboratory Traceability Matrix (Part-B Complete)

| Practical | Milestone / Concept | Implemented Components & Key Features |
|---|---|---|
| **Lab 01** | Application Shell, Enum & Records | `BankInfo.java` (record), `MenuOption.java` (enum), `MiniBank.java` (menu loop with switch expression, Scanner input, re-prompting). |
| **Lab 02** | Encapsulation & Static ID Counters | `Customer.java` (static `customerCounter`, `generateCustomerId()`), `Account.java` (static `accountCounter`, constructors chaining with `this()`, encapsulated `deposit()` / `withdraw()`). |
| **Lab 03** | Object Methods & Nested Classes | `Account.java` (`toString()`, `equals()`, `hashCode()`), `Customer.Address` (static nested class), `Customer.clone()` (deep clone via `Cloneable`), `instanceof` testing. |
| **Lab 04** | Regex Validation & Token Parsing | `Validator.java` (Pattern regex for Mobile, Email, PAN, IFSC), `Command.java` (record), `CommandParser.java` (`split()` parsing), `StatementFormatter.java` (`StringBuilder`). |
| **Lab 05** | Abstract Classes & Polymorphism | Abstract `Account.java` (`interestRate()`, `canWithdraw()`), `SavingsAccount` (4.0% rate, minBalance), `CurrentAccount` (0.0% rate, overdraftLimit), `FixedDepositAccount` (7.0% rate). |
| **Lab 06** | Interfaces, Default Methods & JAR | `Transactable`, `InterestBearing` (default `yearlyInterest()`, `monthlyInterest()`), `WithdrawRule` (functional interface + lambda), `Premium` (marker), modular packaging, `minibank.jar`. |
| **Lab 07** | Custom Annotations & Reflection | `@Id`, `@Positive`, `@MaxLength`, `AnnotationValidator.java` (inspects declared fields by reflection), `@Override`, `@FunctionalInterface`. |
| **Lab 08** | Exception Hierarchy & Shortfall | `BankException`, `InsufficientFundsException` (stores `shortfall`), `AccountNotFoundException`, `InvalidAmountException`, try-catch-finally, `BankSession` (`AutoCloseable`). |
| **Lab 09** | Multithreading & Synchronization | `AccountWorker.java` (`Runnable`), `synchronized` methods on `Account` preventing race conditions across concurrent threads. |
| **Lab 10** | ThreadPools, Deadlocks & Producer-Consumer | `TransactionProcessor.java` (`ExecutorService` pool of 4), consistent lock ordering on account numbers preventing deadlocks, `TransactionQueue` with `wait()` / `notifyAll()`. |
| **Lab 11** | Object Serialization & NIO Reporting | `StatePersister.java` (`ObjectOutputStream`/`InputStream`), `TransactionLog.java` (`Files.write` with `CREATE`/`APPEND`), `ReportGenerator.java` (`Files.newDirectoryStream`, `BufferedReader`). |
| **Lab 12** | Collections Framework & Sorting | `AccountStore.java` (`HashMap`, `ArrayList`), `Account.compareTo()` (`Comparable`), `sortedByBalance()` (`Comparator`), `ConcurrentHashMap` in processor. |
| **Lab 13** | Generic Repository & Bounded Methods | `Repository<T>` (generic CRUD with reflection extracting `@Id`), `@SafeVarargs saveAll()`, bounded generic method `<N extends Number> double average(N[])`. |
| **Lab 14** | Capstone Integration & JUnit 5 Testing | `BankService.java` (wires all layers), `@Audit` reflective logging, `MiniBankTest.java` (passing JUnit 5 tests), persistent state across runs, full documentation. |

---

## 🚀 How to Build and Run

### Prerequisites
- **Java Development Kit (JDK 17 or higher)** (`javac` and `java` available in PATH).
- **Git** for version control.

### Option 1: Using Automation Scripts (Recommended)

#### On macOS / Linux:
```bash
# 1. Build and package minibank.jar
./build.sh

# 2. Run the interactive MiniBank application
./run.sh

# 3. Run all JUnit 5 unit tests
./test.sh
```

#### On Windows:
```cmd
:: 1. Build and package minibank.jar
build.bat

:: 2. Run the interactive MiniBank application
run.bat

:: 3. Run all JUnit 5 unit tests
test.bat
```

### Option 2: Using Standard JDK Command Line

#### 1. Compile the Source Code:
```bash
mkdir -p bin
javac -d bin $(find src -name "*.java")
```

#### 2. Package the Runnable JAR:
```bash
jar --create --file minibank.jar --main-class minibank.MiniBank -C bin .
```

#### 3. Run the Application:
```bash
java -jar minibank.jar
```

#### 4. Run the JUnit 5 Test Suite:
```bash
mkdir -p bin-test
javac -cp "bin:lib/junit-platform-console-standalone.jar" -d bin-test $(find test -name "*.java")
java -jar lib/junit-platform-console-standalone.jar execute -cp "bin:bin-test" --select-class minibank.MiniBankTest
```

---

## 🧭 Console Menu

The interactive application deliberately presents nine options only. Options 1–8 provide
the account operations and batch-processing demonstration; option 9 saves the current
state and exits. The automated checks are run with `test.bat` or `test.sh`, rather than
from the application menu.

---

---
