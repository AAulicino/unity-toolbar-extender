# unity-toolbar-extender

Extend the Unity Toolbar with your own UI code. Please note that it's quite hacky as the code is relying on reflection to access Unity's internal code. It might not work anymore with a new Unity update but is proven to work up to (at least) Unity 2019.1.

Add buttons to quickly access scenes, add sliders, toggles, anything. 

![Imgur](https://i.imgur.com/zFX3cJH.png)

## How to
This example code is shown in action in the gif below. Just hook up your GUI method to ToolbarExtender.LeftToolbarGUI or ToolbarExtender.RightToolbarGUI to draw left and right from the play buttons.
```
	[InitializeOnLoad]
	public class SceneSwitchLeftButton
	{
		static SceneSwitchLeftButton()
		{
			ToolbarExtender.LeftToolbarGUI.Add(OnToolbarGUI);
		}

		static void OnToolbarGUI()
		{
			GUILayout.FlexibleSpace();

			if(GUILayout.Button(new GUIContent("1", "Start Scene 1"), ToolbarStyles.commandButtonStyle))
			{
				SceneHelper.StartScene("Assets/ToolbarExtender/Example/Scenes/Scene1.unity");
			}

			if(GUILayout.Button(new GUIContent("2", "Start Scene 2"), ToolbarStyles.commandButtonStyle))
			{
				SceneHelper.StartScene("Assets/ToolbarExtender/Example/Scenes/Scene2.unity");
			}
		}
	}
```


![Imgur](https://i.imgur.com/DDNfbHW.gif)


## How is it done
The current solution is done by https://github.com/OndrejPetrzilka and uses Unity's new UIElements code and reflection to hook up to the Toolbar's OnGUI callback.
