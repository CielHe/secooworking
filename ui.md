```
-(void)scrollViewWillEndDragging:(UIScrollView *)scrollView withVelocity:(CGPoint)velocity targetContentOffset:(inout CGPoint *)targetContentOffset
{
  scrollView.userInteractionEnabled = NO;
}

-(void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate {
  if (!decelerate) {
    scrollView.userInteractionEnabled = YES;
  }
}

-(void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView {
  _lastXOffset = scrollView.contentOffset.x;
  _currentPage = [self currentPageCalc];
  if(_currentPage == kGuidPageNumber){
    self.enterButton.hidden = NO;
    [self.animTimer setFireDate:[NSDate distantPast]];

  }else {
    self.enterButton.hidden = YES;
    [self.animTimer setFireDate:[NSDate distantFuture]];
  }
  self.lvm_pageControl.currentPage = _currentPage-1;
  scrollView.userInteractionEnabled = YES;
}

```

ps:scrollViewDidEndDecelerating有时没有执行，scrollViewDidEndDragging 中去限制

