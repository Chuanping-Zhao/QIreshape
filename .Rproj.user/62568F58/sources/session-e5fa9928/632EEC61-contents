#' Merge Positive and Negative Metabolomics Data
#'
#' This function merges positive and negative metabolomics data based on the Compound ID.
#' It retains the entry with the highest score for each Compound ID, and if there are duplicates,
#' it then selects the entry with the highest Fragmentation Score.
#'
#' @param posData A data frame containing the positive ion mode metabolomics data.
#' @param negData A data frame containing the negative ion mode metabolomics data.
#'
#' @return A data frame with merged data from positive and negative ion mode, retaining entries
#'         with the highest score and, in case of duplicates, the highest Fragmentation Score.
#' @export
#'
#' @importFrom dplyr group_by arrange filter desc
#' @importFrom magrittr %>%
#'
#' @examples
#' # Assuming posData and negData are data frames with metabolomics data
#'
#' @keywords metabolomics data merging
#'
#' @author Chuanping Zhao
#' @seealso \code{\link[dplyr]{filter}}, \code{\link[dplyr]{arrange}}, \code{\link[dplyr]{group_by}}

QI_mergePos <- function(posData,negData){
  x <- rbind(posData,negData) %>%
  group_by(`Compound.ID`) %>%
    arrange(desc(Score)) %>%
    filter(Score==max(Score)) %>%#相同ID的代谢物有多个时 选择score最大的
    filter(`Fragmentation.Score`==max(`Fragmentation.Score`))##如果筛选完后ID还是有重复，则选择Fragmentation.Score最大的
}
