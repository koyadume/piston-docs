```java
ORMContext ormCtx = ORMContext.getInstance(this, DBConstants.PERSISTENT_UNIT_BOLT);
RequestContext.initORMContext(ormCtx);
try {
	ormCtx.beginTransaction();
	
	Service service = globalDAO.get(Service.class, serviceId);
	if(service.getContainers().size() > 0) {
		for(Container container : service.getContainers()) {
			globalDAO.delete(Container.class, container.getId());
		}
	}
	
	globalDAO.delete(Service.class, serviceId);
	
	ormCtx.commit(this);
} finally {
	RequestContext.clearORMContext(this);
}
```