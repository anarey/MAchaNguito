220 class Class(Node, Registered):
221     ctype = models.CharField(max_length=CF_MAX_LENGTH)
222     c_symbol_prefix = models.CharField(max_length=CF_MAX_LENGTH)
223     fundamental = models.BooleanField(default=False)
224     is_abstract = models.BooleanField(default=False)
225     parent         = models.ForeignKey('Type',     null=True, related_name='cls_parent')
226     unref_func     = models.ForeignKey('Function', null=True, related_name='cls_unref')
227     ref_func       = models.ForeignKey('Function', null=True, related_name='cls_ref')
228     set_value_func = models.ForeignKey('Function', null=True, related_name='cls_set_value')
229     get_value_func = models.ForeignKey('Function', null=True, related_name='cls_get_value')
230 
231     glib_type_struct = models.ForeignKey('Type',   null=True)
232 
233     methods         = models.ManyToManyField('Function', related_name='cls_methods')
234     virtual_methods = models.ManyToManyField('Function', related_name='cls_vmethods')
235     static_methods  = models.ManyToManyField('Function', related_name='cls_smethods')
236     constructors    = models.ManyToManyField('Function', related_name='cls_constructors')
237     signals         = models.ManyToManyField('Signal',   related_name='cls_signals')
238     interfaces      = models.ManyToManyField('Type',     related_name='cls_ifaces')
239 
240     fields          = models.ManyToManyField('Field',    related_name='cls_fields')
241     properties      = models.ManyToManyField('Property', related_name='cls_props')
242     #parent_chain = []


 class Node(Annotated):
 96     c_name = models.CharField (max_length = CF_MAX_LENGTH)
 97     gi_name = models.CharField (max_length = CF_MAX_LENGTH)
 98     namespace = models.ForeignKey('Namespace')
 99     name = models.CharField (max_length = CF_MAX_LENGTH)
100     foreign = models.BooleanField(default=False)
101     #TODO
102     #file_positions = set()
103     def __unicode__ (self):
104         return self.name




 84 class Annotated(models.Model):
 85     version = models.CharField(max_length=CF_VERSION_MAX_LENGTH)
 86     skip = models.BooleanField(default=False)
 87     introspectable = models.BooleanField(default=False)
 88     deprecated_version = models.CharField(max_length=CF_VERSION_MAX_LENGTH)
 89     doc = models.TextField(null=True, blank=True)
 90     deprecated = models.CharField(max_length=CF_MAX_LENGTH)
 91     deprecated_version = models.CharField(max_length=CF_VERSION_MAX_LENGTH)
 92     #TODO
 93     #attributes = [] # (key, value)*


106 class Registered(models.Model):
107     gtype_name = models.CharField (max_length = CF_MAX_LENGTH)
108     #TODO
109 #   get_type = get_type
