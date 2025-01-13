## Table of Contents

- [3. PHP Coding Standards](#php)
  - [3.1. Naming Conventions](#name)
  - [3.2. Constants](#constant)
  - [3.3. Code Format](#format)
  - [3.4. OOP Guidelines](#oop)
  - [3.5. Concurrency](#concurrent)
  - [3.6. Control Statements](#control)
  - [3.7. Others](#other)
  - [3.8. Best Practices Summary](#best-practices)
  - [3.9. Security Guidelines](#security)
  - [3.10. Performance Considerations](#performance)
  - [3.11. Code Documentation](#documentation)
  - [3.12. Error Handling](#error-handling)
  - [3.13. Testing Standards](#testing-standards)
  - [3.14. Version Control](#version-control)
  - [3.15. AI Tool Usage Guidelines](#ai-tool-usage)

<a name="php"></a>
# 3. PHP Coding Standards

<a name="name"></a>
## 3.1. Naming Conventions

1. <font color=bc0008>【Required】</font>Do not mix non-English words and English in code naming, and never use non-ASCII characters directly.

    <font color=977919>Note:</font>Correct English spelling and grammar makes code easier to understand and avoids ambiguity. Non-English naming should be avoided.

    <font color=29965b>Good example:</font>Internationally recognized names like dollar / paypal / netflix / london can be treated as English.

    <font color=fa4113>Bad example:</font>BigDiscountPromotion [discount] / getScoreByName() [score] / (int)someVariable = 3

1. <font color=bc0008>【Required】</font>Use UpperCamelCase for class names.

    <font color=29965b>Good example:</font>XmlService / TcpUdpDeal

    <font color=fa4113>Bad example:</font>XMLService / TCPUDPDeal

1. <font color=bc0008>【Required】</font>Use lowerCamelCase for method names, parameter names, member variables, and local variables.

    <font color=29965b>Good example:</font>localValue / getHttpMessage() / inputUserId

1. <font color=bc0008>【Required】</font>Constants should be all uppercase with words separated by underscores. Make names clear and complete, don't worry about length.

    <font color=29965b>Good example:</font>MAX_STOCK_COUNT / CACHE_EXPIRED_TIME

    <font color=fa4113>Bad example:</font>MAX_COUNT / EXPIRED_TIME

1. <font color=bc0008>【Required】</font>Package names should be in all lowercase, with consecutive words simply concatenated together.

    <font color=29965b>Good example:</font>com.company.mpp.util

    <font color=fa4113>Bad example:</font>com.company.mPP.util

1. <font color=bc0008>【Required】</font>Abstract classes should be prefixed with "Abstract" or "Base".

    <font color=29965b>Good example:</font>AbstractTransactionService / BaseUserService

1. <font color=bc0008>【Required】</font>Exception classes must be suffixed with "Exception".

    <font color=29965b>Good example:</font>ValidationException / BusinessException

1. <font color=bc0008>【Required】</font>Interface names must be prefixed with "I" or suffixed with "Interface".

    <font color=29965b>Good example:</font>IUserService / MessageQueueInterface

1. <font color=bc0008>【Required】</font>Test classes should be suffixed with "Test".

    <font color=29965b>Good example:</font>UserServiceTest / OrderControllerTest

1. <font color=bc0008>【Required】</font>Use verb-noun pairs for method names where appropriate.

    <font color=29965b>Good example:</font>getUser / validateInput / setPassword

    <font color=fa4113>Bad example:</font>user / validation / password

<a name="constant"></a>
## 3.2. Constants

1. <font color=bc0008>【Required】</font>Magic numbers and strings must be defined as constants with descriptive names.

    <font color=29965b>Good example:</font>
    ```php
    const MAX_RETRY_ATTEMPTS = 3;
    const DEFAULT_TIMEOUT_SECONDS = 30;
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    if ($retryCount > 3) { ... }
    $timeout = 30;
    ```

<a name="format"></a>
## 3.3. Code Format

1. <font color=bc0008>【Required】</font>Indentation must use 4 spaces. Do not use tabs.

    <font color=977919>Note:</font>Most IDEs can be configured to automatically convert tabs to spaces.

1. <font color=bc0008>【Required】</font>Opening braces should be placed on the same line as the control structure, with one space before the brace.

    <font color=29965b>Good example:</font>
    ```php
    if ($condition) {
        // code
    }
    
    class MyClass {
        // code
    }
    ```

1. <font color=bc0008>【Required】</font>Each line should generally not exceed 120 characters. If exceeding, break into multiple lines with proper indentation.

    <font color=29965b>Good example:</font>
    ```php
    $result = $this->serviceManager
        ->getUserService()
        ->findByComplexCriteria($param1, $param2);
    ```

1. <font color=bc0008>【Required】</font>Method parameters should be properly formatted when spanning multiple lines.

    <font color=29965b>Good example:</font>
    ```php
    public function someMethod(
        TypeHint $param1,
        TypeHint $param2,
        array $param3 = []
    ) {
        // code
    }
    ```

<a name="oop"></a>
## 3.4. OOP Guidelines

1. <font color=bc0008>【Required】</font>Always use type declarations for method parameters and return types when possible.

    <font color=29965b>Good example:</font>
    ```php
    public function processUser(User $user): bool {
        return true;
    }
    ```

1. <font color=bc0008>【Required】</font>Class properties must declare their visibility (public, protected, or private).

    <font color=29965b>Good example:</font>
    ```php
    class User {
        private string $name;
        protected int $age;
        public bool $isActive;
    }
    ```

1. <font color=bc0008>【Required】</font>Avoid public properties unless absolutely necessary. Use getter and setter methods instead.

    <font color=977919>Note:</font>This promotes encapsulation and allows for future modifications to the implementation.

<a name="concurrent"></a>
## 3.5. Concurrency

1. <font color=bc0008>【Required】</font>When implementing concurrent operations, always use proper locking mechanisms.

    <font color=29965b>Good example:</font>
    ```php
    $lock = flock($fileHandle, LOCK_EX);
    try {
        // Critical section code
    } finally {
        flock($fileHandle, LOCK_UN);
    }
    ```

1. <font color=bc0008>【Required】</font>Use atomic operations when dealing with shared resources.

    <font color=977919>Note:</font>Consider using database transactions or Redis atomic operations when appropriate.

1. <font color=bc0008>【Required】</font>Implement proper error handling and rollback mechanisms for concurrent operations.

<a name="control"></a>
## 3.6. Control Statements

1. <font color=bc0008>【Required】</font>Avoid deep nesting of control structures. Extract complex conditions into well-named methods.

    <font color=29965b>Good example:</font>
    ```php
    if ($this->isValidUser() && $this->hasPermission()) {
        // code
    }
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    if ($user !== null) {
        if ($user->isActive()) {
            if ($user->hasRole('admin')) {
                if (!$user->isLocked()) {
                    // code
                }
            }
        }
    }
    ```

1. <font color=bc0008>【Required】</font>Use early returns to reduce nesting and improve readability.

    <font color=29965b>Good example:</font>
    ```php
    public function processUser(User $user): bool {
        if (!$user->isActive()) {
            return false;
        }
        
        if (!$this->validateUserData($user)) {
            return false;
        }
        
        // Process valid user
        return true;
    }
    ```

1. <font color=bc0008>【Required】</font>Use switch statements instead of multiple if-else when comparing the same variable.

    <font color=29965b>Good example:</font>
    ```php
    switch ($userType) {
        case 'admin':
            $this->handleAdmin();
            break;
        case 'manager':
            $this->handleManager();
            break;
        default:
            $this->handleDefault();
            break;
    }
    ```

<a name="other"></a>
## 3.7. Others

1. <font color=bc0008>【Required】</font>Always use strict comparison operators (=== and !==) unless type coercion is explicitly desired.

    <font color=977919>Note:</font>This prevents unexpected type juggling and improves code reliability.

1. <font color=bc0008>【Required】</font>Use proper error handling with try-catch blocks and avoid suppressing errors.

    <font color=29965b>Good example:</font>
    ```php
    try {
        $result = $this->riskyOperation();
    } catch (SpecificException $e) {
        $this->logger->error('Operation failed', ['error' => $e->getMessage()]);
        throw new BusinessException('Unable to complete operation');
    }
    ```

1. <font color=bc0008>【Required】</font>Always properly sanitize and validate input data.

    <font color=977919>Note:</font>This is crucial for security and data integrity.

<a name="best-practices"></a>
## 3.8. Best Practices Summary

1. <font color=bc0008>【Required】</font>Follow Laravel's coding style guide and PSR-12 standards.

    <font color=977919>Note:</font>Laravel follows PSR-12 with some additional conventions specific to the framework.

1. <font color=bc0008>【Required】</font>Use Laravel's built-in helpers and facades when appropriate.

    <font color=29965b>Good example:</font>
    ```php
    // Using Laravel's helpers
    $value = cache()->remember('key', 3600, fn() => compute_value());
    $path = storage_path('app/files');
    
    // Using Facades
    use Illuminate\Support\Facades\Log;
    Log::info('User logged in', ['user_id' => $user->id]);
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    $value = $_SESSION['cache']['key'];
    $path = __DIR__ . '/storage/app/files';
    ```

1. <font color=bc0008>【Required】</font>Use Laravel's Eloquent ORM features properly.

    <font color=29965b>Good example:</font>
    ```php
    // Using relationships
    public function posts()
    {
        return $this->hasMany(Post::class);
    }
    
    // Using eager loading
    $users = User::with(['posts', 'profile'])->get();
    
    // Using model events
    protected static function booted()
    {
        static::created(function ($user) {
            $user->profile()->create();
        });
    }
    ```

<a name="security"></a>
## 3.9. Security Guidelines

1. <font color=bc0008>【Required】</font>Use Laravel's built-in security features.

    <font color=29965b>Good example:</font>
    ```php
    // CSRF Protection
    @csrf
    
    // XSS Prevention
    {{ $userInput }}
    
    // SQL Injection Prevention
    User::where('email', request()->input('email'))->first();
    
    // Password Hashing
    use Illuminate\Support\Facades\Hash;
    $user->password = Hash::make($request->password);
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    // Don't do this
    DB::raw("SELECT * FROM users WHERE email = '" . $_GET['email'] . "'");
    echo $userInput;
    $user->password = md5($password);
    ```

<a name="performance"></a>
## 3.10. Performance Considerations

1. <font color=bc0008>【Required】</font>Use Laravel's caching system effectively.

    <font color=29965b>Good example:</font>
    ```php
    public function getExpensiveData()
    {
        return cache()->remember('expensive-data', now()->addHours(24), function () {
            return $this->runExpensiveQuery();
        });
    }
    
    // Using tags for cache management
    cache()->tags(['users', 'profiles'])->remember('user-profile', 3600, function () {
        return $this->getUserProfiles();
    });
    ```

1. <font color=bc0008>【Required】</font>Optimize database queries using Laravel's features.

    <font color=29965b>Good example:</font>
    ```php
    // Using chunking for large datasets
    User::chunk(1000, function ($users) {
        foreach ($users as $user) {
            // Process user
        }
    });
    
    // Using lazy loading when appropriate
    $users = User::cursor()->filter(function ($user) {
        return $user->isActive();
    });
    ```

    <font color=977919>Note:</font>Use Laravel's query builder and Eloquent features to prevent N+1 query problems.

<a name="documentation"></a>
## 3.11. Code Documentation

1. <font color=bc0008>【Required】</font>All public methods and classes must have PHPDoc documentation.

    <font color=29965b>Good example:</font>
    ```php
    /**
     * Processes user registration request
     *
     * @param RegisterRequest $request The registration request DTO
     * @return User The newly created user
     * @throws ValidationException When validation fails
     */
    public function register(RegisterRequest $request): User
    ```

1. <font color=bc0008>【Required】</font>Include meaningful descriptions in documentation comments.

    <font color=977919>Note:</font>Documentation should explain the "why" rather than the "what" when the code isn't self-explanatory.

<a name="error-handling"></a>
## 3.12. Error Handling

1. <font color=bc0008>【Required】</font>Use custom exceptions for different error scenarios.

    <font color=29965b>Good example:</font>
    ```php
    class PaymentException extends \Exception {}
    class ValidationException extends \Exception {}
    
    public function processPayment(Payment $payment): void
    {
        if (!$this->isValid($payment)) {
            throw new ValidationException('Invalid payment details');
        }
        
        if (!$this->processTransaction($payment)) {
            throw new PaymentException('Transaction failed');
        }
    }
    ```

1. <font color=bc0008>【Required】</font>Log all exceptions with appropriate context.

    <font color=29965b>Good example:</font>
    ```php
    try {
        $this->processPayment($payment);
    } catch (Exception $e) {
        $this->logger->error('Payment failed', [
            'payment_id' => $payment->getId(),
            'error' => $e->getMessage(),
            'trace' => $e->getTraceAsString()
        ]);
        throw $e;
    }
    ```

<a name="testing-standards"></a>
## 3.13. Testing Standards

1. <font color=bc0008>【Required】</font>Write tests for all new features and bug fixes.

    <font color=29965b>Good example:</font>
    ```php
    public function testUserRegistration(): void
    {
        $userData = [
            'email' => 'user@example.com',
            'password' => 'secure_password'
        ];
        
        $user = $this->userService->register($userData);
        
        $this->assertInstanceOf(User::class, $user);
        $this->assertEquals($userData['email'], $user->getEmail());
    }
    ```

1. <font color=bc0008>【Required】</font>Use meaningful test names that describe the scenario being tested.

    <font color=29965b>Good example:</font>
    ```php
    public function testShouldThrowExceptionWhenEmailAlreadyExists(): void
    public function testShouldCreateUserWithDefaultRole(): void
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    public function testUser(): void
    public function testRegister(): void
    ```

<a name="version-control"></a>
## 3.14. Version Control

1. <font color=bc0008>【Required】</font>Write clear, descriptive commit messages.

    <font color=29965b>Good example:</font>
    ```
    feat: Add user authentication rate limiting
    
    - Implement rate limiting for login attempts
    - Add configuration for threshold and timeout
    - Include unit tests for rate limiter
    ```

1. <font color=bc0008>【Required】</font>Keep commits focused and atomic.

    <font color=977919>Note:</font>Each commit should represent a single logical change.

## 3.15. AI Tool Usage Guidelines

1. <font color=bc0008>【Required】</font>Only use AI tools (ChatGPT, Cursor) when you have a clear understanding of the code and requirements.

    <font color=977919>Note:</font>AI tools should complement your development process, not replace critical thinking and understanding.

    <font color=29965b>Good example:</font>
    ```php
    // Using AI for:
    // - Code formatting and style improvements
    // - Debugging specific error messages
    // - Learning best practices and patterns
    // - Generating repetitive boilerplate code
    // - Documentation improvements
    // - Unit test suggestions
    ```

    <font color=fa4113>Bad example:</font>
    ```php
    // Using AI for:
    // - Writing critical security code
    // - Implementing complex business logic without review
    // - Handling sensitive/proprietary code
    // - Making architectural decisions
    // - Writing code you don't understand
    ```

1. <font color=bc0008>【Required】</font>Always review and test AI-generated code thoroughly.

    <font color=977919>Note:</font>AI tools should be treated as assistants, not replacements for understanding your codebase.

    <font color=29965b>Good example:</font>
    ```php
    // 1. Review generated code for:
    //    - Security vulnerabilities
    //    - Performance implications
    //    - Compliance with coding standards
    //    - Business logic correctness
    
    // 2. Write comprehensive tests:
    public function testAiGeneratedFeature(): void
    {
        // Edge cases
        $this->assertThrows(InvalidInputException::class, fn() => $this->service->process(null));
        
        // Happy path
        $result = $this->service->process($validInput);
        $this->assertEquals($expected, $result);
        
        // Boundary conditions
        $this->assertValidLimits($result);
    }
    ```

1. <font color=bc0008>【Required】</font>Document when AI tools were used for significant code changes.

    <font color=977919>Note:</font>Transparency about AI usage helps with code review and maintenance.

    <font color=29965b>Good example:</font>
    ```php
    /**
     * This method was refactored with AI assistance on 2024-03-14
     * Changes were reviewed and tested by [Developer Name]
     * 
     * AI Usage Details:
     * - Performance optimization of database queries
     * - Added input validation
     * - Generated unit tests
     * 
     * Review Notes:
     * - Validated against security checklist
     * - Load tested with 1000 concurrent users
     * - Approved by senior developer
     */
    public function optimizedMethod(): void
    ```

1. <font color=bc0008>【Required】</font>Follow a structured process when using AI tools.

    <font color=29965b>Good example:</font>
    ```php
    // 1. Define clear requirements before using AI
    // 2. Break down complex tasks into smaller, verifiable chunks
    // 3. Review each AI suggestion independently
    // 4. Test thoroughly before integration
    // 5. Document AI usage and review process
    ```

1. <font color=bc0008>【Required】</font>Never expose sensitive information to AI tools.

    <font color=977919>Note:</font>Be cautious about data privacy and intellectual property when using AI.

    <font color=29965b>Good example:</font>
    ```php
    // Sanitize code before AI review:
    // - Remove API keys and credentials
    // - Replace business-specific logic with generic examples
    // - Mask sensitive data patterns
    // - Use placeholder values for private information
    ```

1. <font color=bc0008>【Required】</font>Maintain version control discipline with AI-generated code.

    <font color=29965b>Good example:</font>
    ```php
    // Commit message:
    // feat(user-service): Optimize database queries [AI-assisted]
    //
    // - Used AI to identify query optimization opportunities
    // - Implemented suggested indexes and eager loading
    // - Added performance tests
    // - Reviewed by: @senior-dev
    // - Performance improvement: 60% reduction in query time
    ```

