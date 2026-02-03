# Code Refactoring Prompt

Use this prompt when restructuring existing code to improve quality without changing functionality.

## Objective
Improve code quality, maintainability, and performance while preserving existing behavior.

## Refactoring Principles

### When to Refactor
- Code is difficult to understand or modify
- Duplicated code exists in multiple places
- Functions are too long or complex
- Poor naming makes intent unclear
- Testing is difficult due to tight coupling
- Performance bottlenecks identified
- Technical debt is accumulating

### When NOT to Refactor
- Under tight deadline pressure (schedule dedicated refactoring time)
- Without test coverage (write tests first)
- When requirements are unclear (clarify first)
- As part of feature development (separate concerns)

## Refactoring Checklist

### 1. Prepare for Refactoring
- [ ] Ensure comprehensive test coverage exists
- [ ] If tests are missing, write them first
- [ ] Commit all working changes (clean slate)
- [ ] Understand the current behavior completely
- [ ] Identify the specific smell or issue

### 2. Common Code Smells

#### Long Functions
```typescript
// ❌ BAD: 100+ line function doing everything
function processOrder(order) {
  // validate order
  // calculate totals
  // apply discounts
  // process payment
  // update inventory
  // send notifications
  // generate invoice
  // ... 100 more lines
}

// ✅ GOOD: Extracted into smaller, focused functions
function processOrder(order: Order): OrderResult {
  validateOrder(order);
  const totals = calculateOrderTotals(order);
  const payment = processPayment(order, totals);
  updateInventory(order);
  notifyStakeholders(order);
  return generateInvoice(order, payment);
}
```

#### Duplicated Code
```typescript
// ❌ BAD: Same logic in multiple places
function calculateShippingForUSA(weight) {
  if (weight < 1) return 5;
  if (weight < 5) return 10;
  return 15;
}

function calculateShippingForCanada(weight) {
  if (weight < 1) return 5;
  if (weight < 5) return 10;
  return 15;
}

// ✅ GOOD: Extract common logic
const SHIPPING_RATES = [
  { maxWeight: 1, cost: 5 },
  { maxWeight: 5, cost: 10 },
  { maxWeight: Infinity, cost: 15 }
];

function calculateShipping(weight: number): number {
  const rate = SHIPPING_RATES.find(r => weight <= r.maxWeight);
  return rate?.cost ?? 0;
}
```

#### God Objects/Classes
```typescript
// ❌ BAD: Class doing too much
class UserManager {
  authenticateUser() { }
  sendEmail() { }
  processPayment() { }
  generateReport() { }
  logActivity() { }
}

// ✅ GOOD: Separate responsibilities
class AuthenticationService { }
class EmailService { }
class PaymentProcessor { }
class ReportGenerator { }
class ActivityLogger { }
```

#### Magic Numbers
```typescript
// ❌ BAD: Unclear magic numbers
if (user.age < 18 || user.accountBalance < 500) {
  return false;
}

// ✅ GOOD: Named constants
const MIN_AGE = 18;
const MIN_BALANCE = 500;

if (user.age < MIN_AGE || user.accountBalance < MIN_BALANCE) {
  return false;
}
```

#### Deep Nesting
```typescript
// ❌ BAD: 5 levels of nesting
function processData(data) {
  if (data) {
    if (data.items) {
      for (const item of data.items) {
        if (item.isValid) {
          if (item.type === 'premium') {
            // do something
          }
        }
      }
    }
  }
}

// ✅ GOOD: Early returns and extraction
function processData(data?: Data): void {
  if (!data?.items) return;
  
  const validItems = data.items.filter(item => item.isValid);
  const premiumItems = validItems.filter(item => item.type === 'premium');
  
  processPremiumItems(premiumItems);
}
```

## Refactoring Techniques

### Extract Function
Move code into a new function with descriptive name
```typescript
// Before
const total = items.reduce((sum, item) => sum + item.price * item.quantity, 0);
const tax = total * 0.08;
const shipping = total > 100 ? 0 : 10;

// After
function calculateOrderTotal(items: Item[]): number {
  const subtotal = calculateSubtotal(items);
  const tax = calculateTax(subtotal);
  const shipping = calculateShipping(subtotal);
  return subtotal + tax + shipping;
}
```

### Extract Variable
Replace complex expression with named variable
```typescript
// Before
if (user.age >= 18 && user.hasLicense && user.violations < 3) { }

// After
const isEligibleDriver = user.age >= 18 && user.hasLicense && user.violations < 3;
if (isEligibleDriver) { }
```

### Rename for Clarity
```typescript
// Before
function calc(x: number): number { }
let d: Date;
const arr = [1, 2, 3];

// After
function calculateDiscount(price: number): number { }
let deliveryDate: Date;
const orderItems = [1, 2, 3];
```

### Replace Conditional with Polymorphism
```typescript
// Before
class Bird {
  fly() {
    if (this.type === 'penguin') {
      return 'Cannot fly';
    } else if (this.type === 'eagle') {
      return 'Soaring high';
    }
  }
}

// After
interface Bird {
  fly(): string;
}

class Penguin implements Bird {
  fly() { return 'Cannot fly'; }
}

class Eagle implements Bird {
  fly() { return 'Soaring high'; }
}
```

### Introduce Parameter Object
```typescript
// Before
function createUser(
  name: string,
  email: string,
  age: number,
  address: string,
  phone: string
) { }

// After
interface UserData {
  name: string;
  email: string;
  age: number;
  address: string;
  phone: string;
}

function createUser(data: UserData) { }
```

## Refactoring Process

### Step-by-Step Approach
1. **Run all tests** - ensure they pass before starting
2. **Make small change** - one refactoring at a time
3. **Run tests again** - verify behavior unchanged
4. **Commit** - save progress incrementally
5. **Repeat** - continue with next refactoring

### Example: Refactoring Legacy Function

**Before:**
```typescript
function p(d: any) {
  let t = 0;
  for (let i = 0; i < d.length; i++) {
    if (d[i].t === 1) {
      t += d[i].p * d[i].q;
    } else if (d[i].t === 2) {
      t += d[i].p * d[i].q * 0.5;
    }
  }
  if (t > 100) t -= 10;
  return t;
}
```

**Step 1: Add types and rename**
```typescript
interface OrderItem {
  type: number;
  price: number;
  quantity: number;
}

function calculateTotal(items: OrderItem[]): number {
  let total = 0;
  for (let i = 0; i < items.length; i++) {
    if (items[i].type === 1) {
      total += items[i].price * items[i].quantity;
    } else if (items[i].type === 2) {
      total += items[i].price * items[i].quantity * 0.5;
    }
  }
  if (total > 100) total -= 10;
  return total;
}
```

**Step 2: Replace magic numbers**
```typescript
const ITEM_TYPE_REGULAR = 1;
const ITEM_TYPE_DISCOUNTED = 2;
const LARGE_ORDER_THRESHOLD = 100;
const LARGE_ORDER_DISCOUNT = 10;

function calculateTotal(items: OrderItem[]): number {
  let total = 0;
  for (let i = 0; i < items.length; i++) {
    if (items[i].type === ITEM_TYPE_REGULAR) {
      total += items[i].price * items[i].quantity;
    } else if (items[i].type === ITEM_TYPE_DISCOUNTED) {
      total += items[i].price * items[i].quantity * 0.5;
    }
  }
  
  if (total > LARGE_ORDER_THRESHOLD) {
    total -= LARGE_ORDER_DISCOUNT;
  }
  
  return total;
}
```

**Step 3: Extract functions**
```typescript
function calculateItemTotal(item: OrderItem): number {
  const basePrice = item.price * item.quantity;
  
  if (item.type === ITEM_TYPE_DISCOUNTED) {
    return basePrice * 0.5;
  }
  
  return basePrice;
}

function applyLargeOrderDiscount(total: number): number {
  return total > LARGE_ORDER_THRESHOLD 
    ? total - LARGE_ORDER_DISCOUNT 
    : total;
}

function calculateTotal(items: OrderItem[]): number {
  const subtotal = items.reduce((sum, item) => sum + calculateItemTotal(item), 0);
  return applyLargeOrderDiscount(subtotal);
}
```

## Performance Refactoring

### Identify Bottlenecks First
```bash
# Profile before optimizing
npm run test:performance
```

### Common Optimizations
```typescript
// ❌ BAD: N+1 queries
for (const user of users) {
  user.posts = await db.getPosts(user.id);
}

// ✅ GOOD: Single query with JOIN
const usersWithPosts = await db.query(`
  SELECT u.*, json_agg(p.*) as posts
  FROM users u
  LEFT JOIN posts p ON p.user_id = u.id
  GROUP BY u.id
`);

// ❌ BAD: Unnecessary recalculation
array.filter(x => expensiveFunction(x))
     .map(x => expensiveFunction(x));

// ✅ GOOD: Calculate once
const calculated = array.map(x => ({
  value: x,
  result: expensiveFunction(x)
}));
const filtered = calculated.filter(item => item.result);
```

## Checklist Before Completing

- [ ] All tests passing
- [ ] No functionality changed
- [ ] Code is more readable
- [ ] Complexity reduced
- [ ] Performance maintained or improved
- [ ] No new dependencies added unnecessarily
- [ ] Documentation updated if needed
- [ ] Team reviewed changes

## Output Format

```
## Refactoring Summary

**Objective**: [What is being improved]
**Approach**: [High-level strategy]

## Changes Made

### Before
[Original code snippet]
**Issues**: [List of smells/problems]

### After
[Refactored code]
**Improvements**: [List of improvements]

## Testing

[Confirmation that tests pass]

## Impact

- Readability: [Better/Same]
- Maintainability: [Better/Same]
- Performance: [Better/Same/Measured difference]
- Test Coverage: [Maintained/Improved]
```
