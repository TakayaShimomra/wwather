
- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
    
    
    //24時間前のunix時間取得
    double currentDate = [[NSDate date] timeIntervalSince1970];
    int x = 86400;
    
    
    NSLog(@"%f",currentDate - x);


    
    //前日の気温データの取得
    NSString *zenhan = @"http://api.openweathermap.org/data/2.5/history/city?id=1850147&type=hour&start=";
    
    NSString *kouhan= [NSString stringWithFormat:@"%f&cnt=1", currentDate - x];

    NSString *api = [ zenhan stringByAppendingString:kouhan];
    
    NSLog(@"%@",api);
    
    
    //前日の気温をjsonで取得
    
    NSData *data = [[NSData alloc] initWithContentsOfURL:[NSURL URLWithString:api]];
    
    NSError *error;
    NSMutableDictionary *parsedData = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingMutableContainers error:&error];
    NSLog  (@"parseData: %@", parsedData[@"list"][0][@"main"][@"temp_max"]);
    
    NSString *print = [[NSString alloc] initWithFormat:@"%@", parsedData[@"list"][0][@"main"][@"temp_max"]] ;
    NSLog(@"%@", print );
    
    
    //当日の気温データの取得
    
    NSString *zenhan2 = @"http://api.openweathermap.org/data/2.5/history/city?id=1850147&type=hour&start=";
    
    NSString *ato= [NSString stringWithFormat:@"%f&cnt=1", currentDate];
   
    NSString *api2 = [zenhan2 stringByAppendingString:ato];
    
    NSLog(@"%@",api2);
    
    
    //当日の気温をjsonで取得
    NSData *data2 = [[NSData alloc] initWithContentsOfURL:[NSURL URLWithString:api2]];
    
    NSLog(@"%@",data2);
    
    NSMutableDictionary *parse = [NSJSONSerialization JSONObjectWithData:data2 options:NSJSONReadingAllowFragments|NSJSONReadingMutableContainers|NSJSONReadingMutableLeaves  error:&error];
    
  
    NSLog  (@"%@", parse[@"list"][0][@"main"][@"temp_max"]);
    
    NSString *print2 = [[NSString alloc] initWithFormat:@"%@", parse[@"list"][0][@"main"][@"temp_max"]];
    
    NSLog(@"%@",print2);
