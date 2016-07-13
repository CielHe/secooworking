```
- (NSString *)_lvm_convertToPresentDateFromAPIDate:(NSString *)origin withFormat:(NSString *)format {
  if (!format) {
    format = @"yyyy-MM-dd HH:mm:ss";
  }
  NSDateFormatter *dateFormatter = [NSDateFormatter new];
  dateFormatter.dateFormat = format;
  NSDate *convDate = [NSDate dateWithTimeIntervalSince1970:
  (NSTimeInterval)(origin.longLongValue/1000)];
  return [dateFormatter stringFromDate:convDate];
}
```

