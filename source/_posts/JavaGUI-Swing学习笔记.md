---
title: JavaGUI_Swing学习笔记
date: 2018-07-18 19:45:02
tags: [Java,笔记]
preview: https://raw.githubusercontent.com/Laurence-042/Resources/master/jpg/anim/yande.re%20361109%20rem_(re_zero)%20weapon.jpg
---
<!--more-->
## JButton点击事件
```Java
//为变量名为btn的按钮添加点击事件
btn.addActionListener(new ActionListener(){
    @Override
    public void actionPerformed(ActionEvent arg0) {
        System.out.print("Button Clicked");
    }           
});//没错，这么5大行玩意是一条语句，是个匿名内部类，并重写了addActionListener的actionPerformed方法
```
[此段代码为转载，并为了突出重点做了一些修改，可点击此处查看来源](https://www.cnblogs.com/shocker/archive/2012/07/19/2598653.html)

## JTable表格的数据来源
不太推荐用这个，还是用JTextArea配合JScrollPane灵活性更高一些也更方便（还没有坑爹的上限200条的限制）
```Java
JTable table = new JTable(obj, columnNames);
/*
obj为二维数组，表示表格的数据来源
比如
Object[][] obj = new Object[2][6];
用此处的obj作数据源的表格将是一个2行6列的表格

columnNames为一维数组，表示第一行的对数据含义的解释（比如“姓名”，“年龄”等等）
当然，columnName的元素数应和obj的列数相同
*/
```
[此段代码为转载，并为了突出重点做了一些修改，可点击此处查看来源](https://blog.csdn.net/caihanyuan/article/details/7320434)

## JTextArea配合JScrollPane展示数据
```Java
JScrollPane scrollPane = new JScrollPane();
scrollPane.setBounds(0, 0, 326, 209);
mainPanel.add(scrollPane);
// 主界面的数据展示区
JTextArea mainTextArea = new JTextArea();
scrollPane.setViewportView(mainTextArea);
```
可以使用以下代码进行数据填充,Student可以为任意数据存储单元
```Java
StringBuffer sb = new StringBuffer();
for (Student st : students) {
    sb.append(st.toString()).append("\n");
}
ta.setText(sb.toString());
ta.setEditable(false);
```
[此段代码主要为老师给的，自己在上面根据需要改了改，没有链接](http://localhost:4000/)

## JOptionPane的几种样式
```Java
JOptionPane.showMessageDialog(null, "我是普通提示框！╮(╯▽╰)╭");  

JOptionPane.showMessageDialog(null, "我是警告提示框！╮(╯▽╰)╭", "标题",JOptionPane.WARNING_MESSAGE);  

JOptionPane.showMessageDialog(null, "我是错误提示框！╮(╯▽╰)╭", "标题",JOptionPane.ERROR_MESSAGE); 

JOptionPane.showMessageDialog(null, "我是最基本提示框！╮(╯▽╰)╭", "标题",JOptionPane.PLAIN_MESSAGE);

int n = JOptionPane.showConfirmDialog(null, "你会了吗?", "标题",JOptionPane.YES_NO_OPTION); //返回值为0或1

Object[] options ={ "必须是", "当然是" };  //自定义按钮上的文字
int m = JOptionPane.showOptionDialog(null, "钓鱼岛是中国的吗？", "标题",JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE, null, options, options[0]);  

Object[] obj2 ={ "路人甲", "路人乙", "路人丙" };  
String s = (String) JOptionPane.showInputDialog(null,"请选择你的身份:\n", "身份", JOptionPane.PLAIN_MESSAGE, new ImageIcon("icon.png"), obj2, "足球");

JOptionPane.showInputDialog(null,"请输入：\n","title",JOptionPane.PLAIN_MESSAGE); 
```
[此段代码为转载，并为了突出重点做了一些修改，可点击此处查看来源](https://blog.csdn.net/c1481118216/article/details/51921521)

## JFreeChart与JPanel结合
下面的类的作用是创建一个容纳图像的panel
```Java
class ImagePanel extends JPanel {

    /**
     * 用于展示统计数据时使用的JFreeChart生成的图片 图片大小和这个panel的大小一致
     */
    private static final long serialVersionUID = 1L;

    private BufferedImage image;

    public ImagePanel() {
        super();
    }

    public void setImage(BufferedImage image) {
        this.image = image;
    }

    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        g.setColor(Color.white);

        if (null != image) {
            this.setSize(image.getWidth(this), image.getHeight(this));
            g.fill3DRect(0, 0, image.getWidth(this), image.getHeight(this), true);
            g.drawImage(image, 0, 0, null, this);
            setPreferredSize(new Dimension(image.getWidth(this), image.getHeight(this)));
        }
    }
}
```
为了生成这个图片，我们需要一个dataset来存储图表所用的信息，以生成十个柱的统计学生BMI值分布的柱状图的方法为例
```Java
public static IntervalXYDataset createDataset(ArrayList<Student> students) {
    // 创建用于展示柱状图的Dataset
    XYSeriesCollection seriesCollection = new XYSeriesCollection();
    XYSeries series1 = new XYSeries("BMI Statistics");

    // 获取最大最小值以及它们的差，用于生成十个数据区间
    float max = getMaxBmi(students);
    float min = getMinBmi(students);
    float size = (max - min) / 10;
    float nowLower = min;
    int nowPos = 0;// 代表当前在bmi数组的位置

    // 创建一个排好序的储存全部学生bmi的数组，以免影响到学生对象原本的排序
    float[] bmi = new float[students.size()];
    for (int i = 0; i < bmi.length; i++) {
        bmi[i] = students.get(i).getBmi();
    }
    Arrays.sort(bmi);

    // 分成十个区间，每个区间的最小值当作代表值
    for (int i = 0; i < 10; i++) {
        int num = 0;

        if (i == 9) {// 若无此判断，在最后一次循环里会因算法问题无法获取正确的人数
            num = bmi.length - nowPos;
            series1.add(nowLower, num);
        } else {
            for (int j = nowPos; j < bmi.length; j++) {
                if (bmi[j] > nowLower + size) {
                    num = j - nowPos;
                    nowPos = j;
                    break;
                }
            }
            series1.add(nowLower, num);
            nowLower = nowLower + size;
        }

    }
    seriesCollection.addSeries(series1);
    return new XYBarDataset(seriesCollection, 0.9);
}
```

为了方便随时更新这个图表的图片，我们还需要一个用于更新的方法  
这个方法里的*data*，*chart*，“image”是我那个主类里存储相应数据的成员变量，分别存储dataset，生成图表所用的chart和这个chart转化的图像  
而statisticsImagePanel则是我实例化的一个ImagePanel对象，就是上面说的那个可以挂在Jpanel下面的，用来展示图表的panel
```Java
public void flushChartImage() {
    // 刷新统计的图片
    data = createDataset(students);
    chart = ChartFactory.createXYBarChart("BMI Statistics", "Intervals", false, "Number of Students", data,
            PlotOrientation.VERTICAL, true, false, false);
    image = chart.createBufferedImage(statisticsImagePanel.getBounds().width,
            statisticsImagePanel.getBounds().height, BufferedImage.TYPE_INT_RGB, null);

    statisticsImagePanel.setImage(image);
}
```

现在只要把下面一段代码加到你想生成这个统计图表的位置就行了，显然我准备把这个图表挂在statisticsPanel这个panel下面，你需要根据自己的需要选择生成的位置
```Java
ImagePanel statisticsImagePanel = new ImagePanel();
statisticsImagePanel.setBounds(10, 34, 409, 188);
statisticsPanel.add(statisticsImagePanel);
```
其实想起来也不算很难，说白了关键其实就是“chart图表->图片构造器->图片->容纳图片的panel”这么个转化途径，自己写一遍你就会发现······  
这玩意真™麻烦，而且也不算很常用，用的时候再看一下再Ctrl+C一下再Ctrl+V一下就好了嘛（笑）   

[此段代码主要为老师给的，自己在上面根据需要改了改，没有链接](http://localhost:4000/)

## JMenu的使用
```Java
JMenuBar jMenuBar = new JMenuBar();
JMenu jMenu = new JMenu("菜单");
JMenuItem item1 = new JMenuItem("主界面");
item1.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent arg0) {
        switchPanel(mainPanel);
    }
});
JMenuItem item2 = new JMenuItem("输入");
item2.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent arg0) {
        switchPanel(inputPanel);
    }
});
JMenuItem item3 = new JMenuItem("维护");
item3.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent arg0) {
        switchPanel(maintainPanel);
    }
});
JMenuItem item4 = new JMenuItem("统计");
item4.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent arg0) {
        switchPanel(statisticsPanel);
    }
});
jMenu.add(item1);
jMenu.add(item2);
jMenu.add(item3);
jMenu.add(item4);
jMenuBar.add(jMenu);
// 这里是添加标题栏
frame.setJMenuBar(jMenuBar);
```
其中，`switchPanel()`是一个自己写的函数，用于在同一窗口切换Panel，很简单就能实现（但用百度有点难查到）
```Java
private void switchPanel(JPanel panel) {
    frame.getContentPane().removeAll();
    frame.getContentPane().add(panel);
    frame.getContentPane().revalidate();
    frame.getContentPane().repaint();
}
```
<!--more-->
