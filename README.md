# Xcode CodeSnippets

Useful set of Xcode Code Snippets.  
open Terminal.app, clone this repository into the following path:

Usage:

    cd ~/Library/Developer/Xcode/UserData/CodeSnippets
    git clone git@github.com:youngshook/XcodeCodeSnippets.git .

open Xcode.app. Enjoy :)
## Xcode CodeSnippets Descriptions

**addAChildViewcontroller.codesnippet**  (Add a child ViewController)  
Shortcut: `childController`  
Description: `Adds a child ViewController to self`  

    UIViewController *newController = <#newController#>;
        [newController willMoveToParentViewController:self];
        [self addChildViewController:newController];
        [self.contentView addSubview:newController.view];
        [newController didMoveToParentViewController:self];

**animationBlockAllParameters.codesnippet**  (Animation block all parameters)  
Shortcut: `animfullblock`  
Description: `animfullblock`  

    UIViewAnimationOptions options = UIViewAnimationOptionBeginFromCurrentState | UIViewAnimationOptionAllowUserInteraction;
    [UIView animateWithDuration:<#duration#> delay:0.0 options:options animations:^{
        <#code#>
                } completion:^(BOOL finished) {
                }];

**assignProperty.codesnippet**  (Assign Property)  
Shortcut: `pna`  
Description: `pna`  

    @property (nonatomic, assign) <#Type#> <#Property Name#>;

**aTodoMarkedWithMyInitials.codesnippet**  (A todo marked with my initials)  
Shortcut: `todo`  
Description: `todo`  

    // TODO (YoungShook): <#Note#>

**blockMethodWithNoParameters.codesnippet**  (Block: Method with no parameters)  
Shortcut: `blocknoparamsmethod`  
Description: `blocknoparamsmethod`  

    - (void)<#methodName#>WithCompletionBlock:(void (^)())completionBlock {
        
        if (completionBlock) {
            completionBlock();
        }
    }
    

**blockMethodWithParameters.codesnippet**  (Block: Method with parameters)  
Shortcut: `blockmethod`  
Description: `blockmethod`  

    - (void)<#methodName#>WithCompletionBlock:(void (^)(NSString *message, NSError *error))completionBlock {
        NSString *message = nil;
        NSError *error = nil;
        
        if (completionBlock) {
            completionBlock(message, error);
        }
    }
    

**blockSafeSelfPointer.codesnippet**  (Block safe self pointer)  
Shortcut: `bs`  
Description: `A weak pointer to self (for usage in blocks).`  

    __weak typeof(self) blockSelf = self;

**blockVariableWithName.codesnippet**  (Block Variable with Name)  
Shortcut: `block_named_variable`  
Description: `block_named_variable`  

    void (^<#blockName#>)(NSData *data) =  ^void (NSData *data, NSError *error) {      
                };

**blockWeakSelf.codesnippet**  (block weak self)  
Shortcut: `bws`  
Description: `bws`  

    #define BBlockWeakObject(o) __weak __typeof__((__typeof__(o))o)
    
    #define BBlockWeakSelf BBlockWeakObject(self)

**classExtension.codesnippet**  (Class Extension)  
Shortcut: `class_extension`  
Description: `class_extension`  

    #pragma mark - Class Extension
    #pragma mark - 
    
    @interface <#Class Name#> ()
    
    @end

**copyProperty.codesnippet**  (Copy Property)  
Shortcut: `pnc`  
Description: `pnc`  

    @property (nonatomic, copy) <#Class name#> *<#Property Name#>;

**debuglogAnObject.codesnippet**  (DebugLog an Object)  
Shortcut: `dl_object`  
Description: `dl_object`  

    NSLog(@"<#name#>: %@", <#name#>);

**debugLogMethod.codesnippet**  (Debug Log Method)  
Shortcut: `dl_method`  
Description: `dl_method`  

    NSLog(@"%@", NSStringFromSelector(_cmd));

**defineMacros.codesnippet**  (Define Macros)  
Shortcut: `define_macros`  
Description: `define_macros`  

    #define SYSTEM_VERSION_GREATER_THAN_OR_EQUAL_TO(v)  ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] != NSOrderedAscending)
    
    #define LOG_FRAME(label, frame) DebugLog(@"%@: %f, %f, %f, %f", label, frame.origin.x, frame.origin.y, frame.size.width, frame.size.height)
    #define LOG_SIZE(label, size) DebugLog(@"%f, %f, %f", label, size.width, size.height)
    #define LOG_POINT(label, point) DebugLog(@"%@: %f, %f", label, point.x, point.y)
    #define LOG_OFFSET(label, offset) DebugLog(@"%@: %f, %f", label, offset.x, offset.y)
    #define LOG_INSET(label, inset) DebugLog(@"%@: %f, %f, %f, %f", label, inset.top, inset.left, inset.bottom, inset.right)

**defineSingletonMacro.codesnippet**  (Define Singleton Macro)  
Shortcut: `define_singleton_macro`  
Description: `define_singleton_macro`  

    // Adapted to ARC from Matt Gallagher of CocoaWithLove
    // Insert into in .pch to use in a project
    #define SYNTHESIZE_SINGLETON_FOR_HEADER(classname) \
    + (classname *)sharedInstance;
    
    #define SYNTHESIZE_SINGLETON_FOR_CLASS(classname) \
     \
        static classname *sharedInstance = nil; \
        static dispatch_once_t onceToken; \
     \
    + (classname *)sharedInstance \
    { \
        dispatch_once(&onceToken, ^{ \
            sharedInstance = [[classname alloc] init]; \
        }); \
    	 \
    	return sharedInstance; \
    } \
     \

**deleteDocument.codesnippet**  (Delete Document)  
Shortcut: `document_delete`  
Description: `document_delete`  

    - (void)deleteDocument:(UIDocument *)document withCompletionBlock:(void (^)())completionBlock {
        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_LOW, 0), ^{
            
            NSError *fileCoordinatorError = nil;
            
            [[[NSFileCoordinator alloc] initWithFilePresenter:nil] coordinateWritingItemAtURL:document.fileURL options:NSFileCoordinatorWritingForDeleting error:&fileCoordinatorError byAccessor:^(NSURL *newURL) {
    
                // extra check to ensure coordinator is not running on main thread
                NSAssert(![NSThread isMainThread], @"Must be not be on main thread");
    
                // create a fresh instance of NSFileManager since it is not thread-safe
                NSFileManager *fileManager = [[NSFileManager alloc] init];
                NSError *error = nil;
                if (![fileManager removeItemAtURL:newURL error:&error]) {
                    NSLog(@"Error: %@", error);
                    // TODO handle the error
                }
                
                if (completionBlock) {
                    completionBlock();
                }
            }];
        });
    }

**deprecated.codesnippet**  (Deprecated)  
Shortcut: `deprecated`  
Description: `deprecated`  

    __attribute__ ((deprecated))

**directoryExists.codesnippet**  (Directory Exists)  
Shortcut: `directory_exists`  
Description: `directory_exists`  

        BOOL isDirectory = TRUE;
        BOOL exists = [[NSFileManager defaultManager] fileExistsAtPath:url.path isDirectory:&isDirectory];

**drawImageMethod.codesnippet**  (Draw Image Method)  
Shortcut: `draw_image_method`  
Description: `draw_image_method`  

    - (UIImage *)<#method name#> {
        static UIImage *image = nil;
        static dispatch_once_t onceToken;
        dispatch_once(&onceToken, ^{
            UIGraphicsBeginImageContextWithOptions(CGSizeMake(<#width#>, <#height#>), NO, 0.0f);
            
            // insert code from PaintCode here
            <#code#>
            
            image = UIGraphicsGetImageFromCurrentImageContext();
            UIGraphicsEndImageContext();
            
        });
        return image;
    }

**errorCreation.codesnippet**  (Error creation)  
Shortcut: `error_create`  
Description: `error_create`  

    NSDictionary *userInfo = @{NSLocalizedDescriptionKey : @"<#error description#>"};
    NSError *error = [NSError errorWithDomain:@"<#domain#>" code:<#errorcode#> userInfo:userInfo];

**fileIsExist.codesnippet**  (File is exist)  
Shortcut: `fie`  
Description: `fie`  

    - (BOOL)isFileExist:(NSString *)filePath
    {
        NSFileManager *fileManager = [NSFileManager defaultManager];
        return [fileManager fileExistsAtPath:filePath];
    }

**fileIsRemove.codesnippet**  (File is remove)  
Shortcut: `fir`  
Description: `fir`  

    - (BOOL)removeFile:(NSString *)filePath
    {
        NSFileManager *fileManager = [NSFileManager defaultManager];
        return [fileManager removeItemAtPath:filePath error:nil];
    }

**fileIsSize.codesnippet**  (File is size)  
Shortcut: `fis`  
Description: `fis`  

    - (unsigned long long)isFileSize:(NSString *)filePath
    {
    NSFileManager *fileManager = [[NSFileManager alloc] init];
    NSDictionary *dict = [fileManager attributesOfItemAtPath:filePath error:nil];
    return (unsigned long long)[dict fileSize];
    }
    

**fuckingblockmethod.codesnippet**  (FuckingBlockMethod)  
Shortcut: `fuckingBlockMethod`  
Description: `Declares a method that takes a block as its first parameter`  

    - (void)someMethodThatTakesABlock:(<#returnType#> (^)(<#parameterTypes#>))<#parameterName#>
    {
        
    }

**fuckingblockproperty.codesnippet**  (FuckingBlockProperty)  
Shortcut: `fuckingBlockProperty`  
Description: `Delcares a block as a fucking property`  

    @property (nonatomic, copy) <#returnType#> (^<#blockName#>)(<#parameterTypes#>);

**fuckingblocktypedef.codesnippet**  (FuckingBlockTypedef)  
Shortcut: `fuckingBlockTypedef`  
Description: `Typedefs a fucking block`  

    typedef <#returnType#> (^<#TypeName#>)(<#parameterTypes#>);

**fuckingblockvariable.codesnippet**  (FuckingBlockVariable)  
Shortcut: `fuckingBlockVariable`  
Description: `Declares a block as a fucking local variable`  

    <#returnType#> (^<#blockName#>)(<#parameterTypes#>) = ^<#returnType#>(<#parameters#>) {
        <#code#>
    };

**gcdAsyncCurrentQueue.codesnippet**  (GCD: Async Current Queue)  
Shortcut: `gcd_async_current`  
Description: `gcd_async_current`  

    
        dispatch_queue_t callerQueue = dispatch_get_current_queue();
    dispatch_queue_t <#queueName#> = dispatch_queue_create("<#queueLabel#>", NULL);
    dispatch_async(<#queueName#>, ^{
            
            // Do async work
            
            dispatch_async(callerQueue, ^{
                
                // Finish work on the caller's queue
                
            });
        });
    dispatch_release(<#queueName#>);
    

**gcdAsyncGlobalQueue.codesnippet**  (GCD: Async Global Queue )  
Shortcut: `gcd_async_global`  
Description: `gcd_async_global`  

        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            // Heavy task
            dispatch_async(dispatch_get_main_queue(), ^{
                // Update UI
            });
            
        });

**gcdAsyncWait.codesnippet**  (GCD: Async Wait)  
Shortcut: `gcd_async_wait`  
Description: `gcd_async_wait`  

    
    // do not use
    dispatch_queue_t <#queue#> = dispatch_queue_create("<#queue#>", NULL);
        dispatch_async(queue, ^ {
            // do async work
        });
        
        // do more work concurrently
    dispatch_sync(<#queue#>, ^{}); // wait for async block to finish
    //dispatch_release(<#queue#>); // not needed for ARC
    

**gcdDefaultPriorityQueue.codesnippet**  (GCD: Default priority queue)  
Shortcut: `gcd_default_priority_queue`  
Description: `gcd_default_priority_queue`  

    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        <#code#>
    });

**gcdDispatchAfter.codesnippet**  (GCD: Dispatch After)  
Shortcut: `gcd_dispatchafter`  
Description: `gcd_dispatchafter`  

    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, <#ms#> * NSEC_PER_SEC), dispatch_get_main_queue(), ^{
        <#code#>
        });

**gcdGetQueueLabel.codesnippet**  (GCD: Get Queue Label)  
Shortcut: `gcd_getqueuelabel`  
Description: `gcd_getqueuelabel`  

    NSString *queueLabel = [NSString stringWithCString: dispatch_queue_get_label(dispatch_get_current_queue())encoding:NSUTF8StringEncoding];

**gcdMainQueue.codesnippet**  (GCD: Main Queue)  
Shortcut: `gcd_main_queue`  
Description: `gcd_main_queue`  

        dispatch_async(dispatch_get_main_queue(), ^{
            <#code#>
        });

**gcdRunOnMainQueue.codesnippet**  (GCD: Run on Main Queue)  
Shortcut: `define_gcd_run_on_main_queue`  
Description: `define_gcd_run_on_main_queue`  

    #define gcd_run_on_main_queue(block) \
        if ([NSThread isMainThread]) \
            block(); \
        else \
            dispatch_sync(dispatch_get_main_queue(), block); \
    

**gcdRunWithHighPriorityQueue.codesnippet**  (GCD: Run with high priority queue)  
Shortcut: `gcd_high_priority_queue`  
Description: `gcd_high_priority_queue`  

        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_HIGH, 0),^{
            ￼
        });

**gcdRunWithLowPriorityQueue.codesnippet**  (GCD: Run with low priority queue)  
Shortcut: `gcd_low_priority_queue`  
Description: `gcd_low_priority_queue`  

        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_LOW, 0), ^{
            ￼
        });

**gcdWaitForBlocks.codesnippet**  (GCD: Wait for Blocks)  
Shortcut: `gcd_wait_for_blocks`  
Description: `gcd_wait_for_blocks`  

        @autoreleasepool {
            dispatch_queue_t queue = dispatch_queue_create("<#queue name#>", 0);
            dispatch_sync(queue,  ^(){
                // insert sync code
            });
            dispatch_async(queue, ^(){
                // insert async code
            });
            // wait for queue
            dispatch_barrier_sync(queue, ^(){
                // insert completion code
            });
        }

**getLibraryCachesPath.codesnippet**  (get Library Caches Path)  
Shortcut: `librarycaches`  
Description: `librarycaches`  

                    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);
                    NSString *LibraryDirectory = [paths objectAtIndex:0];

**heightForMainScreen.codesnippet**  (Height for main screen)  
Shortcut: `height_main_screen`  
Description: `height_main_screen`  

    CGRectGetHeight([[UIScreen mainScreen] bounds])

**heightForViewControllerSView.codesnippet**  (Height for View Controller's View)  
Shortcut: `height_for_vc_view`  
Description: `height_for_vc_view`  

    CGRectGetHeight(self.view.frame)

**imageDraw.codesnippet**  (Image Draw)  
Shortcut: `draw_image`  
Description: `draw_image`  

    UIGraphicsBeginImageContextWithOptions(CGSizeMake(<#width#>￼￼, <#height#>￼￼), NO, 0.0f);
    
        // insert code from PaintCode here
        ￼￼<#code#>
    
        image = UIGraphicsGetImageFromCurrentImageContext();
        UIGraphicsEndImageContext();
        //use image

**imageResizeToMax.codesnippet**  (Image Resize to Max)  
Shortcut: `image_resize_to_max`  
Description: `image_resize_to_max`  

    - (UIImage *)resizeImage:(UIImage *)image toMaximumSize:(CGSize)maxSize {
        CGFloat widthRatio = maxSize.width / image.size.width;
        CGFloat heightRatio = maxSize.height / image.size.height;
        CGFloat scaleRatio = widthRatio < heightRatio ? widthRatio : heightRatio;
        CGSize newSize = CGSizeMake(image.size.width * scaleRatio, image.size.height * scaleRatio);
        
        UIGraphicsBeginImageContextWithOptions(newSize, NO, image.scale);
        [image drawInRect:CGRectMake(0, 0, newSize.width, newSize.height)];
        UIImage *resizedImage = UIGraphicsGetImageFromCurrentImageContext();
        UIGraphicsEndImageContext();
        
        return resizedImage;
    }

**isBackgroundSupported.codesnippet**  (Is Background Supported)  
Shortcut: `isBackgroundSupported`  
Description: `isBackgroundSupported`  

    - (BOOL)isBackgroundSupported {
        UIDevice* device = [UIDevice currentDevice];
        BOOL backgroundSupported = NO;
        if ([device respondsToSelector:@selector(isMultitaskingSupported)]) {
            backgroundSupported = device.multitaskingSupported;
        }
        
        return backgroundSupported;
    }

**isDateAfterOtherDate.codesnippet**  (Is date after other date)  
Shortcut: `date_is_after`  
Description: `date_is_after`  

    
        BOOL isAfter = [[NSDate distantFuture] compare:[NSDate distantPast]] == NSOrderedDescending;

**isViewControllerVisible.codesnippet**  (Is View Controller Visible)  
Shortcut: `isviewcontrollervisible`  
Description: `isviewcontrollervisible`  

        if (self.isViewLoaded && self.view.window) {
            // viewController is visible
        }

**keyboard.codesnippet**  (keyboard)  
Shortcut: `keyboardhide`  
Description: `keyboardhide`  

    -(void)textFieldDidBeginEditing:(UITextField *)sender
    {
        if ([sender isEqual:_textField])
        {
            //move the main view, so that the keyboard does not hide it.
            if  (self.view.frame.origin.y >= 0)
            {
                [self setViewMovedUp:YES];
            }
        }
    }
    
    //method to move the view up/down whenever the keyboard is shown/dismissed
    -(void)setViewMovedUp:(BOOL)movedUp
    {
        [UIView beginAnimations:nil context:NULL];
        [UIView setAnimationDuration:0.5]; // if you want to slide up the view
        
        CGRect rect = self.view.frame;
        if (movedUp)
        {
            // 1. move the view's origin up so that the text field that will be hidden come above the keyboard 
            // 2. increase the size of the view so that the area behind the keyboard is covered up.
            rect.origin.y -= kOFFSET_FOR_KEYBOARD;
            rect.size.height += kOFFSET_FOR_KEYBOARD;
        }
        else
        {
            // revert back to the normal state.
            rect.origin.y += kOFFSET_FOR_KEYBOARD;
            rect.size.height -= kOFFSET_FOR_KEYBOARD;
        }
        self.view.frame = rect;
        
        [UIView commitAnimations];
    }
    
    
    - (void)keyboardWillShow:(NSNotification *)notif
    {
        //keyboard will be shown now. depending for which textfield is active, move up or move down the view appropriately
        
        if ([_textField isFirstResponder] && self.view.frame.origin.y >= 0)
        {
            [self setViewMovedUp:YES];
        }
        else if (![_textField isFirstResponder] && self.view.frame.origin.y < 0)
        {
            [self setViewMovedUp:NO];
        }
    }
    
    
    - (void)viewWillAppear:(BOOL)animated
    {
        // register for keyboard notifications
        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(keyboardWillShow:)
                                                     name:UIKeyboardWillShowNotification object:self.view.window];
    }
    
    - (void)viewWillDisappear:(BOOL)animated
    {
        // unregister for keyboard notifications while not visible.
        [[NSNotificationCenter defaultCenter] removeObserver:self name:UIKeyboardWillShowNotification object:nil];
    }

**localizedString.codesnippet**  (Localized String)  
Shortcut: `localized_string`  
Description: `localized_string`  

    NSLocalizedString(@"<#value#>", <#comment string or nil#>)

**logFonts.codesnippet**  (Log Fonts)  
Shortcut: `log_fonts`  
Description: `log_fonts`  

    - (void)logFonts {
        for (id familyName in [UIFont familyNames]) {
            DebugLog(@"Family Name: %@", familyName);
            for (id fontName in [UIFont fontNamesForFamilyName:familyName]) {
                DebugLog(@"Font Name: %@", fontName);
            }
        }
    }

**maassertDefined.codesnippet**  (MAAssert Defined)  
Shortcut: `maassert_defined`  
Description: `maassert_defined`  

    #ifndef NS_BLOCK_ASSERTIONS
    
    // Credit: http://sstools.co/maassert
    #define MAAssert(expression, ...) \
    do { \
    if(!(expression)) { \
    NSLog(@"Assertion failure: %s in %s on line %s:%d. %@", #expression, __func__, __FILE__, __LINE__, [NSString stringWithFormat: @"" __VA_ARGS__]); \
    abort(); \
    } \
    } while(0)
    
    #else
    
    #define MAAssert(expression, ...)
    
    #endif
    
    

**mainThreadAssertion.codesnippet**  (Main Thread Assertion)  
Shortcut: `main_thread_assert`  
Description: `main_thread_assert`  

    MAAssert([NSThread isMainThread], @"Must be main thread");

**methodPragmaMark.codesnippet**  (Method Pragma Mark)  
Shortcut: `mk`  
Description: `mk`  

    #pragma mark <#Label#>

**methodReturnVoid.codesnippet**  (Method Return Void)  
Shortcut: `method`  
Description: `method`  

    - (void)<#methodName#> {
        <#DO#>
    }

**myCodeSnippet.codesnippet**  (My Code Snippet)  
Shortcut: ``  
Description: ``  

    #pragma mark - UIViewController
    
    - (void)viewDidLoad {
        [super viewDidLoad];
    }
    
    - (void)viewDidUnload {
        [super viewDidUnload];
    }
    
    - (void)viewWillAppear:(BOOL)animated {
        [super viewWillAppear:animated];
    }
    
    - (void)viewDidAppear:(BOOL)animated {
        [super viewDidAppear:animated];
    }
    
    - (void)viewWillDisappear:(BOOL)animated {
    	[super viewWillDisappear:animated];
    }
    
    - (void)viewDidDisappear:(BOOL)animated {
    	[super viewDidDisappear:animated];
    }

**noticationHandler.codesnippet**  (Notication: Handler)  
Shortcut: `notification_handler`  
Description: `notification_handler`  

    - (void)<#method name#>:(NSNotification *)notification {
    }

**notificationAddObserver.codesnippet**  (Notification: Add Observer)  
Shortcut: `notification_observe`  
Description: `notification_observe`  

    	[[NSNotificationCenter defaultCenter] addObserver:self
                                                 selector:@selector(<#selector#>)
                                                     name:<#notification name#>
    				 object:nil];

**notificationNamedBlock.codesnippet**  (Notification: Named Block)  
Shortcut: `notification_named_block`  
Description: `notification_named_block`  

    void (^<#blockName#>)(NSNotification *notification) =  ^void (NSNotification *notification) {
                };

**notificationObserveByNameWithBlock.codesnippet**  (Notification: Observe by Name with Block)  
Shortcut: `notification_observewithblock`  
Description: `notification_observewithblock`  

    
    self.<#name#>Observer = [[NSNotificationCenter defaultCenter] addObserverForName:<#name#> 
                                                      object:nil 
                                                       queue:[NSOperationQueue mainQueue] 
                                                  usingBlock:^(NSNotification *notification) {
                                                      <#code#>
                                                  }];

**notificationPost.codesnippet**  (Notification: Post)  
Shortcut: `notification_post`  
Description: `notification_post`  

    [[NSNotificationCenter defaultCenter] postNotificationName:<#notification name#> object:<#nil or userInfo dictionary#>];

**notificationPostWithUserInfo.codesnippet**  (Notification: Post with User Info)  
Shortcut: `notification_post_with_userinfo`  
Description: `notification_post_with_userinfo`  

    
    NSDictionary *userInfo = [NSDictionary dictionaryWithObject:<#object#> 
                                                         forKey:<#key#>];
    [[NSNotificationCenter defaultCenter] postNotificationName:<#name#> 
                                                                object:nil
                                                              userInfo:userInfo];

**notificationRemoveBlockObserver.codesnippet**  (Notification: Remove Block Observer)  
Shortcut: `notification_remove_block_observer`  
Description: `notification_remove_block_observer`  

    
    [[NSNotificationCenter defaultCenter] removeObserver:self.<#observer property#> 
                                                    name:<#notification name#> 
                                                      object:nil];

**notificationRemoveObserver.codesnippet**  (Notification: Remove Observer)  
Shortcut: `notification_remove`  
Description: `notification_remove`  

    	[[NSNotificationCenter defaultCenter] removeObserver:self 
                                                        name:<#notification name#> 
                                                      object:nil];

**nslog.codesnippet**  (NSLog)  
Shortcut: `lg`  
Description: `lg`  

    NSLog(@"<#Log#>");

**performBlockAfterDelay.codesnippet**  (Perform Block After Delay)  
Shortcut: `block_peform_after_delay`  
Description: `block_peform_after_delay`  

    
    - (void)performBlock:(void (^)(void))block afterDelay:(NSTimeInterval)delay {
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, delay * NSEC_PER_SEC), dispatch_get_main_queue(), block);
    }

**prepareForSegue.codesnippet**  (Prepare for Segue)  
Shortcut: `prepareforsegue`  
Description: `prepareforsegue`  

    - (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
        DebugLog(@"segue: %@", segue.identifier);
    }
    

**pushAViewcontroller.codesnippet**  (Push a ViewController)  
Shortcut: `push`  
Description: `Pushes a newly created ViewController on the current NavigationController`  

    <#UIViewController#>* viewController = [[<#UIViewController#> alloc] init];
        [self.navigationController pushViewController:viewController animated:YES];

**retainProperty.codesnippet**  (Retain Property)  
Shortcut: `pnr`  
Description: `pnr`  

    @property (nonatomic, retain) <#Type#> <#Property Name#>;

**runOnMainThread.codesnippet**  (Run on Main Thread)  
Shortcut: `run_on_main_thread`  
Description: `run_on_main_thread`  

    void runOnMainQueueWithoutDeadlocking(void (^block)(void))
    {
        if ([NSThread isMainThread])
        {
            block();
        }
        else
        {
            dispatch_sync(dispatch_get_main_queue(), block);
        }
    }

**sectionHeader.codesnippet**  (Section Header)  
Shortcut: `pmk`  
Description: `pmk`  

    #pragma mark - <#Section Name#>
    #pragma mark - 

**setupAutoresizingOfAView.codesnippet**  (Setup autoresizing of a view)  
Shortcut: `autoresizing`  
Description: `Set the autoresizing flags of a view`  

    <#view#>.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;

**sharedSingleton.codesnippet**  (Shared Singleton)  
Shortcut: `single`  
Description: `single`  

    + (instancetype)shared<#name#> {
        static <#class#> *_shared<#name#> = nil;
        static dispatch_once_t onceToken;
        dispatch_once(&onceToken, ^{
            _shared<#name#> = <#initializer#>;
        });
        
        return _shared<#name#>;
    }
    

**singleImplementation.codesnippet**  (single implementation)  
Shortcut: `sgi`  
Description: `sgi`  

    + (id)share<#ClassName#>
    {
        static <#ClassName#> *<#className#> = nil;
        static dispatch_once_t onceToken;
    
        dispatch_once(&onceToken, ^{ <#className#> = [[self alloc] init];});
        return <#className#>;
    }
    
    - (id)init
    {
        self = [super init];
        if (self) {
            
        }
        return self;
    }

**stringConstantHeader.codesnippet**  (String Constant Header)  
Shortcut: `string_constant_header`  
Description: `string_constant_header`  

    extern NSString * const <#name#>;

**stringConstantImplementation.codesnippet**  (String Constant Implementation)  
Shortcut: `string_constant_imp`  
Description: `string_constant_imp`  

    NSString * const <#name#> = @"<#value#>";

**stringContains.codesnippet**  (String Contains)  
Shortcut: `string_contains`  
Description: `string_contains`  

    [<#string#> rangeOfString:@"<#match#>"].location != NSNotFound

**strongProperty.codesnippet**  (Strong Property)  
Shortcut: `sdah`  
Description: `sdah`  

    @property (nonatomic, strong) <#Class name#> *<#Property Name#>;

**suppressDeprecationWarning.codesnippet**  (Suppress deprecation warning)  
Shortcut: `suppress_deprecation_warnings`  
Description: `suppress_deprecation_warnings`  

    #pragma GCC diagnostic ignored "-Wdeprecated-declarations"
    // deprecated method call
    #pragma GCC diagnostic warning "-Wdeprecated-declarations"

**udidGenerator.codesnippet**  (UDID Generator)  
Shortcut: `udid_create`  
Description: `udid_create`  

        CFUUIDRef uuid = CFUUIDCreate(NULL);
        CFStringRef uuidStr = CFUUIDCreateString(NULL, uuid);
        NSString *uniqueIdentifier = [NSString stringWithFormat:@"%@", uuidStr];

**uicollectionviewDatesource.codesnippet**  (UICollectionView DateSource)  
Shortcut: `cvds`  
Description: `cvds`  

    
    #pragma mark - UICollectionViewDataSource
    
    - (NSInteger)collectionView:(UICollectionView *)collectionView
    numberOfItemsInSection:(NSInteger)section
    {
        return <#numberOfItemsInSection#>;
    }
    
    - (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView
    cellForItemAtIndexPath:(NSIndexPath *)indexPath
    {
        UICollectionViewCell *cell = [collectionView dequeueReusableCellWithReuseIdentifier:<#reuseIdentifier#> forIndexPath:indexPath];
        
        [self configureCell:cell forItemAtIndexPath:indexPath];
        
        return cell;
    }
    
    - (void)configureCell:(UICollectionViewCell *)cell
    forItemAtIndexPath:(NSIndexPath *)indexPath
    {
        <# statements #>
    }
    

**uicontroleventtouchupinside.codesnippet**  (UIControlEventTouchUpInside)  
Shortcut: `tu`  
Description: `tu`  

    UIControlEventTouchUpInside

**uiimageviewAlloc.codesnippet**  (UIImageView Alloc)  
Shortcut: `imv`  
Description: `imv`  

    [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"<#image name#>"]]

**uitableviewDelegates.codesnippet**  (UITableView Delegates)  
Shortcut: `tvds`  
Description: `tvds`  

    
    #pragma mark - UITableViewDataSource
    #pragma mark -
    
    - (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
        return <#number#>;
    }
    
    - (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
        return <#number#>;
    }
    
    - (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
        static NSString *CellIdentifier = @"<#identifier#>";
        UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier forIndexPath:indexPath];
        
        return cell;
    }
    
    - (void)configureCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath {
        // TODO configure cell
    }
    
    #pragma mark - UITableViewDelegate
    #pragma mark -
    
    - (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    }
    
    

**uiviewAnimateBlock.codesnippet**  (UIView Animate Block)  
Shortcut: `animblock`  
Description: `animblock`  

     [UIView animateWithDuration:<#secs#> animations:^{
            <#code#>
        } completion:^(BOOL finished) {
        }];

**uiviewcontrollerLifecycel.codesnippet**  (UIViewController LifeCycel)  
Shortcut: `lifecycel`  
Description: `lifecycel`  

    #pragma mark - UIViewController
    
    - (void)viewDidLoad {
        [super viewDidLoad];
    }
    
    - (void)viewDidUnload {
        [super viewDidUnload];
    }
    
    - (void)viewWillAppear:(BOOL)animated {
        [super viewWillAppear:animated];
    }
    
    - (void)viewDidAppear:(BOOL)animated {
        [super viewDidAppear:animated];
    }
    
    - (void)viewWillDisappear:(BOOL)animated {
    	[super viewWillDisappear:animated];
    }
    
    - (void)viewDidDisappear:(BOOL)animated {
    	[super viewDidDisappear:animated];
    }

**uiwebviewdelegate.codesnippet**  (UIWebViewDelegate)  
Shortcut: `webviewdelegate`  
Description: `webviewdelegate`  

    #pragma mark - UIWebViewDelegate
    
    - (void)webView:(UIWebView *)webView didFailLoadWithError:(NSError *)error {
        if (error.code != NSURLErrorCancelled) {
            <#Do#>
        }
    }
    
    - (void)webViewDidFinishLoad:(UIWebView *)webView {
        <#Do#>
    }
    
    - (void)webViewDidStartLoad:(UIWebView *)webView {
        <#Do#>
    }
    
    - (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {
        <#Do#>
        return YES;
    }

**viewDidDisappear.codesnippet**  (View Did Disappear)  
Shortcut: `viewdiddisappear`  
Description: `viewdiddisappear`  

    - (void)viewDidDisappear:(BOOL)animated {
        [super viewDidDisappear:animated];
    }

**viewDidLoad.codesnippet**  (View Did Load)  
Shortcut: `viewdidload`  
Description: `viewdidload`  

    - (void)viewDidLoad {
        [super viewDidLoad];
    }

**viewWillAppear.codesnippet**  (View Will Appear)  
Shortcut: `viewwillappear`  
Description: `viewwillappear`  

    - (void)viewWillAppear:(BOOL)animated {
        [super viewWillAppear:animated];
    }

**viewWillDisappear.codesnippet**  (View Will Disappear)  
Shortcut: `viewwilldissappear`  
Description: `viewwilldissappear`  

    - (void)viewWillDisappear:(BOOL)animated {
        [super viewWillDisappear:animated];
    }

**weakProperty.codesnippet**  (Weak Property)  
Shortcut: `pnw`  
Description: `pnw`  

    @property (nonatomic, weak) <#Class name#> *<#Property Name#>;

