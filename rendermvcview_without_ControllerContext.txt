public  string GetRazorViewAsString(string view, object model)
        {
            var st = new StringWriter();
            var context = new HttpContextWrapper(HttpContext.Current);
            //var context = ControllerContext.HttpContext;
            var routeData = new RouteData();
            var controllerContext = new ControllerContext(new RequestContext(context, routeData), new FakeController());
            var razor = new RazorView(controllerContext, view, null, false, null);
            razor.Render(new ViewContext(controllerContext, razor, new ViewDataDictionary(model), new TempDataDictionary(), st), st);
            return st.ToString();
        }