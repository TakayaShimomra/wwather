- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
    
    
    
    //24時間前のunix時間取得
    double currentDate = [[NSDate date] timeIntervalSince1970];
    
    int x = 86400;
    
    
    NSLog(@"%f",currentDate - x);
    
    
    //気温データの取得
    
  
   //上で取得したUNIX時間をURLに代入したいが、うまくいかない。
    
NSData *data = [[NSData alloc] initWithContentsOfURL:
              
[NSURL URLWithString:@"http://api.openweathermap.org/data/2.5/history/city?id=1850147&type=hour&start=1405762954&cnt=1"]];
    
    
    
    NSError *error;
    NSMutableDictionary *parsedData = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingMutableContainers error:&error];
    
   NSLog  (@"%@", parsedData[@"main"][@"temp"]);
    
    
    //ココで上手く「temp_max」の数字が抜き出せないです。
    
   NSString *print = [[NSString alloc] initWithFormat:@"%@",parsedData[@"main"][@"temp"]] ;
    
   
    
    int retInt = [print intValue];
    
    int n = 273.15;
    
    
   NSLog(@"%d", retInt - n );
    
    NSLog(@"%@", print );
    
    
   NSString *ondo = [[NSString alloc] initWithFormat:@"%d",abs(retInt - n)] ;
    
    
    
    self.kion.text = ondo;
