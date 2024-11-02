
# Create Multi-Project Templates in Visual Studio (Windows)

This document provides a detailed guide on how to create multi-project templates in Visual Studio.

## Overview
Multi-project templates allow for the creation of project solutions that include two or more projects. Each project within the template is defined with its specific settings, allowing for a robust and flexible solution setup.

### Key Points
- Multi-project templates are packaged in a `.zip` file.
- They require a root `.vstemplate` file indicating the type as `ProjectGroup`.
- Individual projects within the template are linked using `ProjectTemplateLink` elements.

## Basic Structure of a Multi-Project Template
Below is an example of a basic `vstemplate` structure:

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## Example with Solution Folders
To organize projects into solution folders:

```xml
<VSTemplate Version="2.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <SolutionFolder Name="Math Classes">
                <ProjectTemplateLink ProjectName="MathClassLib1">
                    MathClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="MathClassLib2">
                    MathClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
            <SolutionFolder Name="Graphics Classes">
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">
                    GraphicsClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">
                    GraphicsClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

### Additional Tips
- Ensure each project template has its own `.vstemplate` file.
- Use the `CopyParameters` attribute to pass template parameters between linked projects.
- If you want the main template to show up without the individual project templates appearing, mark the inner templates as hidden:
```xml
<VSTemplate Type="Project" ...>
    <TemplateData>
        ...
        <Hidden>true</Hidden>
    </TemplateData>
    ...
</VSTemplate>
```

### References
For more information, see:
- [Creating project and item templates](https://learn.microsoft.com/en-us/visualstudio/ide/creating-project-and-item-templates?view=vs-2022)
- [Visual Studio template schema reference (extensibility)](https://learn.microsoft.com/en-us/visualstudio/extensibility/visual-studio-template-schema-reference?view=vs-2022)

---

*This document is based on the [official Microsoft guide](https://learn.microsoft.com/en-us/visualstudio/ide/how-to-create-multi-project-templates?view=vs-2022#create-multi-project-templates).*
