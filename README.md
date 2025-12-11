rm(list = ls())
if(!require(ggplot2)) install.packages("ggplot2", dependencies = TRUE)
if(!require(RColorBrewer)) install.packages("RColorBrewer", dependencies = TRUE)
library(ggplot2)
library(RColorBrewer)
library(scales)
employee <- read.csv("employee.csv", stringsAsFactors = FALSE)
employee$Gender <- as.factor(employee$Gender)
employee$LeaveOrNot <- factor(employee$LeaveOrNot, levels = c(0,1), labels = c("Stayed","Left"))
table_gender_leave <- table(Gender = employee$Gender, Leave = employee$LeaveOrNot)
print(table_gender_leave)
p <- ggplot(employee, aes(x = Gender, fill = LeaveOrNot)) +
  geom_bar(position = "fill", width = 0.6, color = "black") +  # bars with border
  scale_fill_brewer(palette = "Set2") +  # soft, pleasant colors
  scale_y_continuous(labels = scales::percent_format()) +
  labs(
    title = "Proportion of Employees Leaving by Gender",
    subtitle = "Based on Company Dataset",
    x = "Gender",
    y = "Proportion (%)",
    fill = "Leave Status"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(face = "bold", size = 16, hjust = 0.5),
    plot.subtitle = element_text(size = 12, hjust = 0.5),
    axis.title = element_text(face = "bold"),
    legend.title = element_text(face = "bold"),
    legend.position = "top"
  )
  scale_y_continuous(labels = scales::percent_format()) +
  labs(
    title = "Proportion of Employees Leaving by Gender",
    subtitle = "Based on Company Dataset",
    x = "Gender",
    y = "Proportion (%)",
    fill = "Leave Status"
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(face = "bold", size = 16, hjust = 0.5),
    plot.subtitle = element_text(size = 12, hjust = 0.5),
    axis.title = element_text(face = "bold"),
    legend.title = element_text(face = "bold"),
    legend.position = "top"
  )

# Print bar plot
print(p)
mosaicplot(table_gender_leave,
           main = "Mosaic Plot of Leave Status by Gender",
           xlab = "Gender",
           ylab = "Leave Status",
           color = c("#66c2a5","#fc8d62"))  # custom colors for Stayed/Left

