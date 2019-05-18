@Override
public Result detailOrderList(OrderParam orderParam) {
QueryWrapper<OrderDetail> queryWrapper = new QueryWrapper<>();
queryWrapper.eq("app_code", orderParam.getAppCode());

// 查询条件
if(!StringUtil.isEmpty(orderParam.getOrderViceNumber())){
queryWrapper.eq("mian_order_number", orderParam.getOrderNumber());
}
if(!StringUtil.isEmpty(orderParam.getOrderViceNumber())){
queryWrapper.eq("vice_order_number", orderParam.getOrderViceNumber());
}
if(!StringUtil.isEmpty(orderParam.getOrderDetailNumber())){
queryWrapper.eq("detail_number", orderParam.getOrderDetailNumber());
}
if(!StringUtil.isEmpty(orderParam.getMerchantId())){
queryWrapper.eq("merchant_code", orderParam.getMerchantId());
}
if(!StringUtil.isEmpty(orderParam.getItemCode())){
queryWrapper.eq("good_code", orderParam.getItemCode());
}
if (!StringUtil.isEmpty(orderParam.getStartTime())) {
queryWrapper.ge("create_date", orderParam.getStartTime());
}
if (!StringUtil.isEmpty(orderParam.getEndTime())) {
queryWrapper.le("create_date", orderParam.getEndTime());
}
if (!StringUtil.isEmpty(orderParam.getMinPrice())) {
queryWrapper.ge("order_amount", orderParam.getMinPrice());
}
if (!StringUtil.isEmpty(orderParam.getMaxPrice())) {
queryWrapper.le("order_amount", orderParam.getMaxPrice());
}
if (!StringUtil.isEmpty(orderParam.getOrderState())) {
queryWrapper.eq("order_state", orderParam.getOrderState());
}
Page<OrderDetail> page = new Page<>(orderParam.getPageNum(), orderParam.getPageSize());
IPage<OrderDetail> userIPage = page(page, queryWrapper);
return Result.success(userIPage);
}
