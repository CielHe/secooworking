在每一View的layer层中有一个mask属性，他就是专门来设置该View的遮罩效果的。该mask本身也是一个layer层。我们只需要生成一个自定义的layer，然后覆盖在需要遮罩的View上面即可。问题就归于如何生成入上图所示的不规则图片的Layer。CAShapeLayer可以根据几个点的依次连线，产生一个闭合空间的layer。如下图所示：

```
@implementation CAShapeLayer (ViewMask)

+ (instancetype)createMaskLayerWithView : (UIView *)view{

    CGFloat viewWidth = CGRectGetWidth(view.frame);
    CGFloat viewHeight = CGRectGetHeight(view.frame);

    CGFloat rightSpace = 10.;
    CGFloat topSpace = 15.;

    CGPoint point1 = CGPointMake(0, 0);
    CGPoint point2 = CGPointMake(viewWidth-rightSpace, 0);
    CGPoint point3 = CGPointMake(viewWidth-rightSpace, topSpace);
    CGPoint point4 = CGPointMake(viewWidth, topSpace);
    CGPoint point5 = CGPointMake(viewWidth-rightSpace, topSpace+10.);
    CGPoint point6 = CGPointMake(viewWidth-rightSpace, viewHeight);
    CGPoint point7 = CGPointMake(0, viewHeight);


    UIBezierPath *path = [UIBezierPath bezierPath];
    [path moveToPoint:point1];
    [path addLineToPoint:point2];
    [path addLineToPoint:point3];
    [path addLineToPoint:point4];
    [path addLineToPoint:point5];
    [path addLineToPoint:point6];
    [path addLineToPoint:point7];
    [path closePath];

    CAShapeLayer *layer = [CAShapeLayer layer];
    layer.path = path.CGPath;

    return layer;
}

@end

```

```
UIView *view = [[UIView alloc] initWithFrame:CGRectMake(40, 50, 80, 100)];
view.backgroundColor = [UIColor orangeColor];
[self.view addSubview:view];

CAShapeLayer *layer = [CAShapeLayer createMaskLayerWithView:view];
view.layer.mask = layer;
```

