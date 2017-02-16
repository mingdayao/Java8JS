# Java8JS

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.script.Invocable;
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class SimpleTest {
	
	public static void main(String[] args) throws ScriptException, NoSuchMethodException {
		
		ScriptEngine engine = new ScriptEngineManager().getEngineByName("nashorn");
		engine.eval(getScript2());
		
		Invocable invocable = (Invocable) engine;
		Object result = invocable.invokeFunction("func", prepareData());
		
		System.out.println(result);
		
		
	}
	
	private static String getScript(){
		String script = "var fun = function(name){"
				+ "print('Hi my name is ' + name);"
				+ "};"
				+ "fun('michael')";
		return script;
	}
	
	private static String getScript2(){
		List<Map<String, Object>> dataList = prepareData();
		
		 
		
		
		String script = 
					      "var func = function(dataList) {"
					    + "print(Object.prototype.toString.call(dataList));"
					    + "var returnList = new java.util.ArrayList();"
					    + "for each (var e in dataList) "
					    + "if(e.gender == 'Male') {"
					    + "   returnList.add(e)"	
					    + "}"
					    + "return returnList"	  
					    + "};";	
			
		
		
		
		return script;
	}
	
	
	private static List<Map<String, Object>> prepareData() {
		
		List<Map<String, Object>> dataList = new ArrayList<Map<String, Object>>();
		
		Map<String, Object> map1 = new HashMap<String, Object>();
		map1.put("name", "Michael");
		map1.put("gender", "Male");
		
		Map<String, Object> map2 = new HashMap<String, Object>();
		map2.put("name", "Sara");
		map2.put("gender", "Female");
		
		Map<String, Object> map3 = new HashMap<String, Object>();
		map3.put("name", "Alex");
		map3.put("gender", "Male");
		
		dataList.add(map1);
		dataList.add(map2);
		dataList.add(map3);
		
		return dataList;
		
	}
	
}

//http://winterbe.com/posts/2014/04/05/java8-nashorn-tutorial/
//http://www.infoq.com/cn/articles/nashorn
