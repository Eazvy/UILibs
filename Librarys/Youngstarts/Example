local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/youngstar"))();

local Window1 = library:CreateWindow("YoungStar's Lib");

Window1:Button("Example Button",function()
  print("YoungStar is cool!");
end);

Window1:Slider("Example Slider",16,100,true,function(X)
  if X then
      print(X)
  end
end);

Window1:Box("Example Box",function(examplebox)
  if examplebox then
      print(examplebox)
  end;
end);

Window1:Toggle("ExampleToggle",function(E)
  ToggleExample = E;
end);

spawn(function()
  while wait() do
      if ToggleExample then
          local Cool = 0
          repeat wait()
          Cool = Cool + 1
          print("YoungStar = Cool")
          until Cool == 10
          break
      end;
  end;
end);
